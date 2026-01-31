# Git Workflow Note: Branching from a Specific Commit and Pushing to Remote

This note documents a **reproducible Git workflow** for creating a new branch from an existing commit (identified by a hash) and pushing it to a remote repository.
This is especially useful for **scientific experiments**, **ablation studies**, and **paper-version control**.

---

## 1. Create a New Branch from a Specific Commit

Assume you already know the commit hash (full or short).

### Option A: Create and switch to the branch (recommended)

```bash
git checkout -b <new-branch-name> <commit-hash>
```

Example:

```bash
git checkout -b exp-v1 3f2a9c7
```

This:

* Creates a new branch `exp-v1`
* Sets its HEAD at commit `3f2a9c7`
* Switches your working directory to this branch

---

### Option B: Modern syntax (Git ≥ 2.23)

```bash
git switch -c <new-branch-name> <commit-hash>
```

Example:

```bash
git switch -c exp-v1 3f2a9c7
```

This is functionally equivalent to `checkout -b`, but semantically clearer.

---

### Option C: Create without switching (less common)

```bash
git branch <new-branch-name> <commit-hash>
```

You must switch manually afterward:

```bash
git checkout <new-branch-name>
```

---

## 2. Push the New Branch to the Remote Repository

After creating and switching to the new branch:

### Recommended (sets upstream)

```bash
git push -u origin <branch-name>
```

Example:

```bash
git push -u origin exp-v1
```

This will:

1. Create `origin/exp-v1` on the remote
2. Link the local branch to the remote branch (upstream)
3. Enable future use of plain `git push` / `git pull`

---

## 3. Verify Branch–Remote Association

```bash
git branch -vv
```

Expected output:

```
* exp-v1 3f2a9c7 [origin/exp-v1] Commit message
```

This confirms that:

* The branch points to the correct commit
* The upstream remote is correctly configured

---

## 4. Pushing to a Differently Named Remote Branch (Optional)

If you want the remote branch name to differ:

```bash
git push -u origin <local-branch>:<remote-branch>
```

Example:

```bash
git push -u origin exp-v1:paper-exp-v1
```

---

## 5. Notes for Experimental Reproducibility

### 5.1 Clean Working Tree Recommended

Before branching, ensure no uncommitted changes:

```bash
git status
```

If needed:

```bash
git stash
```

This avoids accidental coupling between experiments.

---

### 5.2 Typical Research Use Cases

| Use Case                     | Recommended Pattern    |
| ---------------------------- | ---------------------- |
| Re-running an old experiment | `exp-v1`, `exp-v2`     |
| Ablation study               | `ablation-no-reweight` |
| Paper camera-ready freeze    | `paper-freeze`         |
| Bug fix on old results       | `hotfix-exp-v1`        |

---

### 5.3 Best Practice for Papers

* Always record:

  * Branch name
  * Commit hash
  * Tag (if any)
* Prefer **branching over `git reset`**
* Avoid `--force` unless absolutely necessary

---

## 6. Minimal Reproducibility Record (Template)

```text
Experiment ID: Exp-V1
Git Branch: exp-v1
Base Commit: 3f2a9c7
Remote: origin/exp-v1
Description: Reproduce baseline results reported in Section 4.2
```

---

