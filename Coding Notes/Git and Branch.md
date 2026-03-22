# Git: Branching & Experiment Workflow

## Branch from a Specific Commit

```bash
# Recommended (create + switch)
git checkout -b exp-v1 3f2a9c7

# Modern syntax (Git >= 2.23)
git switch -c exp-v1 3f2a9c7

# Create without switching
git branch exp-v1 3f2a9c7
```

---

## Push New Branch to Remote

```bash
git push -u origin exp-v1          # -u sets upstream for future git push/pull
git push -u origin exp-v1:paper-v1  # push to differently named remote branch
```

Verify:
```bash
git branch -vv   # shows: * exp-v1 3f2a9c7 [origin/exp-v1] commit message
```

---

## Experiment Reproducibility Patterns

| Use Case | Branch Name Pattern |
|----------|---------------------|
| Re-run old experiment | `exp-v1`, `exp-v2` |
| Ablation study | `ablation-no-reweight` |
| Paper camera-ready freeze | `paper-freeze` |
| Bug fix on old results | `hotfix-exp-v1` |

**Always record:**
- Branch name + commit hash
- What the branch represents (which paper section/experiment)

---

## Common Operations

```bash
# Clean working tree before branching
git stash           # stash uncommitted changes
git stash pop       # restore after switching

# See all branches (local + remote)
git branch -a

# Delete a branch
git branch -d exp-v1          # local (safe, checks merged)
git push origin --delete exp-v1  # remote

# Merge branch back
git checkout main
git merge exp-v1 --no-ff      # --no-ff preserves branch history
```

---

## Key Rules

- **Prefer branching over `git reset`** — never lose old experiment results
- Avoid `--force` push unless you own the branch entirely
- Run `git status` before creating a new branch — don't carry dirty state across experiments
