# SSH through ASU VPN (split-horizon DNS workaround)

How to reach ASU SCAI DHCP-assigned machines (e.g. `*.scai.dhcp.asu.edu`) over
VSCode Remote-SSH while connected to `sslvpn.asu.edu/2fa` — without losing the
ability to use hostnames.

## The problem

ASU runs two SSL VPN endpoints:

| Endpoint | Mode | Default route | SSH to `*.scai.dhcp.asu.edu` |
|----------|------|---------------|------------------------------|
| `sslvpn.asu.edu/2fa` | split-tunnel | home gateway | **fails** (DNS empty) |
| `sslvpn.asu.edu/tunnel` | full-tunnel | VPN | works |

Under `/2fa` the client gets a VPN-side IP (observed: `172.31.x.x`). ASU's
authoritative DNS applies **split-horizon**: `dhcp.asu.edu` zone exists and
the SOA record is served, but host records in `*.scai.dhcp.asu.edu` are hidden
from this "external" view. `/tunnel` places the client inside the internal
view, so resolution succeeds.

Symptom: VSCode Remote-SSH hangs at connect under `/2fa`; manual `dig` of the
hostname returns `NOERROR` with no answer.

## Root cause, confirmed

Under `/2fa`:

- `ping 129.219.253.100` (authoritative `dhcppw.asu.edu`) — works, ~46 ms via
  `utun4`.
- `dig @129.219.253.100 SOA dhcp.asu.edu` — returns SOA (`aa` flag set).
- `dig @129.219.253.100 A en*.scai.dhcp.asu.edu` — `NOERROR`, empty answer.

Connectivity is fine; DNS view is the blocker. The `10.0.0.0/8` block (which
covers these machines' 10.218.x.x leases) is already routed through the VPN
under `/2fa` — so once the hostname resolves locally, the TCP path works.

## The fix

Pin FQDN → IP in `/etc/hosts`. SSH config keeps using hostnames, so nothing
else changes. A LaunchDaemon automates refresh whenever the VPN connects.

### Architecture

```
launchd (WatchPaths on /etc/resolv.conf, /var/run/resolv.conf)
   │  (triggers when macOS rewrites DNS config — happens on VPN up/down)
   ▼
refresh-scai-hosts-guard   # checks 172.31.x.x utun + pings ASU DNS + debounce
   ▼
refresh-scai-hosts-core    # dig each *.scai.dhcp.asu.edu from ~/.ssh/config
                           # rewrite managed block in /etc/hosts
                           # flush dscacheutil + mDNSResponder
```

Design points:

- **SSH config is the source of truth.** Scripts parse `HostName` lines from
  `~/.ssh/config`. Adding a new machine = add an SSH entry, nothing else.
- **`/etc/hosts` block is marker-delimited** (`# BEGIN scai-dhcp` / `# END
  scai-dhcp`) so non-managed entries are never touched.
- **Resilience:**
  - If 0 hosts resolve (e.g. accidentally triggered under `/2fa`), the file
    is left untouched — prior entries survive.
  - Offline hosts keep their last-known IP until explicitly refreshed.
  - No-op detection: if the managed block is already identical to what would
    be written, skip the write (keeps backup count sane).
- **Written for bash 3.2** (macOS system `/bin/bash`). No associative arrays
  (`declare -A`) — uses temp files for lookups.

### Files

| Path | Role |
|------|------|
| `~/bin/refresh-scai-hosts` | User wrapper; `exec sudo` → core |
| `~/bin/refresh-scai-hosts-core` | Root worker; updates `/etc/hosts` |
| `~/bin/refresh-scai-hosts-guard` | Daemon entry; VPN check + 60 s debounce |
| `/Library/LaunchDaemons/edu.asu.scai-hosts-refresh.plist` | LaunchDaemon |
| `/var/log/scai-hosts-refresh.log` | Log (appended by both guard and core) |
| `/var/run/scai-hosts.stamp` | Debounce timestamp |

### Install (one-time)

After putting the three scripts in `~/bin/` and the plist in `~/bin/` as a
staging copy:

```bash
chmod +x ~/bin/refresh-scai-hosts ~/bin/refresh-scai-hosts-core ~/bin/refresh-scai-hosts-guard
plutil -lint ~/bin/edu.asu.scai-hosts-refresh.plist

sudo install -o root -g wheel -m 644 \
  ~/bin/edu.asu.scai-hosts-refresh.plist \
  /Library/LaunchDaemons/edu.asu.scai-hosts-refresh.plist \
&& sudo launchctl bootstrap system \
  /Library/LaunchDaemons/edu.asu.scai-hosts-refresh.plist \
&& sudo touch /var/log/scai-hosts-refresh.log \
&& sudo chown root:wheel /var/log/scai-hosts-refresh.log
```

### First population

Offline machines have no DNS record, so connect to `/tunnel` once with all
GPU boxes powered on, then either let the daemon fire or force it:

```bash
sudo touch /etc/resolv.conf       # triggers WatchPaths
tail -20 /var/log/scai-hosts-refresh.log
```

Expected: `guard: VPN active; running core` → `updated /etc/hosts (resolved=N)`.

After that, switch back to `/2fa` — hostnames still resolve from the local
file and SSH (including VSCode Remote-SSH) works normally.

## Operations

### Manual refresh

```bash
refresh-scai-hosts
```

(Requires `~/bin` on `$PATH`; add via `echo 'export PATH="$HOME/bin:$PATH"'
>> ~/.zshrc`.)

### Inspect managed entries

```bash
awk '/# BEGIN scai-dhcp/,/# END scai-dhcp/' /etc/hosts
```

### Watch live

```bash
tail -f /var/log/scai-hosts-refresh.log
```

### Force daemon to re-run

```bash
sudo touch /etc/resolv.conf
```

### Daemon status

```bash
sudo launchctl print system/edu.asu.scai-hosts-refresh | head -40
```

### Uninstall

```bash
sudo launchctl bootout system/edu.asu.scai-hosts-refresh
sudo rm /Library/LaunchDaemons/edu.asu.scai-hosts-refresh.plist
# Optional: strip the managed block from /etc/hosts
sudo sed -i '' '/# BEGIN scai-dhcp/,/# END scai-dhcp/d' /etc/hosts
```

## Diagnostic commands worth remembering

These are the commands that *actually identified* the problem during the
original debugging session; keep them for future network issues.

```bash
# Which interface carries default traffic right now?
route -n get default | grep -E 'interface|gateway'

# Is a specific target routed through the VPN tunnel?
route -n get 10.218.110.8 | grep -E 'interface|gateway'

# Which DNS servers is macOS consulting, for which search domains?
scutil --dns | grep -E 'resolver|nameserver|search|domain' | head

# Check zone existence (authoritative answer) vs actual host answer —
# empty answer + SOA present + aa flag = split-horizon, not connectivity.
dig @129.219.253.100 SOA dhcp.asu.edu
dig @129.219.253.100 A  en4228357l.scai.dhcp.asu.edu
```

## Gotchas

- **Do not use `declare -A`** or any bash 4+ feature in these scripts —
  macOS ships bash 3.2 at `/bin/bash` and the scripts start with
  `#!/bin/bash`. If you need associative lookup, write to a temp file and
  use `awk '$2==FQDN {print $1}'` (that is how `-core` does it).
- **DHCP-assigned IPs drift.** When a machine comes back up after a long
  shutdown it may get a different 10.218.x.x. The daemon catches this on
  the next VPN reconnect automatically. If you're on `/2fa` and a
  connection starts failing, first thing to check: `dig @129.219.253.100
  +short <hostname>` under `/tunnel` and re-run `refresh-scai-hosts`.
- **`interactivecomments` is off in zsh by default.** Pasting lines that
  start with `#` into an interactive zsh prompt gives
  `zsh: command not found: #`. Either drop the comments or
  `setopt interactivecomments`.
- **`WatchPaths` fires on every DNS config rewrite**, not only on VPN
  events. The 60 s debounce in `-guard` handles the burst that happens
  during a single connect (several rewrites within ~1 s).
- **Why not `scutil` notifications instead of `WatchPaths`?** `scutil -w`
  is cleaner in principle but needs a long-lived watcher process. A
  one-shot launchd trigger plus the debounce is simpler and has the same
  end-to-end behavior for this use case.

## Rejected alternatives (and why)

- **Always use `/tunnel`.** Works, but pushes all non-ASU traffic through
  the VPN — slower, and some consumer services geo-block ASU IPs.
- **Hardcode IPs in `~/.ssh/config`.** Loses the meaningful alias and
  breaks every time DHCP hands out a new lease.
- **Dnsmasq with per-domain forwarders.** Would solve the view problem if
  ASU also operated an internal-view resolver reachable from external
  VPN IPs — it doesn't (confirmed: queries against `dhcppw.asu.edu`
  directly still come back empty from the `/2fa` IP).
- **`mDNSResponder` custom resolver entry** (`/etc/resolver/scai.dhcp.asu.edu`).
  Same blocker as above — the view is keyed on client IP, not on which
  resolver you query.
