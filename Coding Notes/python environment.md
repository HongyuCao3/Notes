# Python Environment Management

## Conda: Windows → Linux Migration

### The Problem with `pip freeze`
- `pip freeze` may output `package @ file:///C:/...` paths — these are local build paths that **don't exist on other machines**
- Using such a `requirements.txt` on Linux will fail

### Recommended: `environment.yml`

**Export on Windows:**
```bash
conda env export > environment.yml
```

**Clean up before sharing:**
- Remove `prefix:` field (machine-specific path)
- Remove build strings like `=py39h6cxxx0_0` (platform-specific)
- Remove Windows-only packages (e.g., `win_inet_pton`)

**Minimal cross-platform `environment.yml`:**
```yaml
name: myproject
channels:
  - pytorch
  - conda-forge
  - defaults
dependencies:
  - python=3.9
  - numpy
  - pandas
  - scikit-learn
  - pytorch::pytorch
  - pip:
    - some-pip-only-package
```

**Recreate on Linux:**
```bash
conda env create -f environment.yml
```

---

### Alternative: Filter `pip freeze` (pure pip projects)

```bash
# Linux/macOS
pip freeze | grep -v "@" > requirements.txt

# Windows PowerShell
pip freeze | Select-String -NotMatch "@" > requirements.txt
```

---

### Advanced: `conda-lock` (fully reproducible + cross-platform)

```bash
conda install -c conda-forge conda-lock
conda-lock -f environment.yml --platform linux-64 --platform osx-64
conda-lock install conda-lock.yml
```

---

## PyTorch Installation (platform-specific)

| Platform | Command |
|----------|---------|
| Linux CPU | `conda install pytorch torchvision torchaudio cpuonly -c pytorch` |
| Linux CUDA | `conda install pytorch torchvision torchaudio pytorch-cuda=11.8 -c pytorch -c nvidia` |
| Windows | Use the [PyTorch install selector](https://pytorch.org/get-started/locally/) |

- Always use channel-qualified installs: `pytorch::pytorch` in `environment.yml` to avoid version conflicts

---

## Key Rules

- **Don't** use `pip freeze` across platforms — use `environment.yml` instead
- **Don't** require exact build versions — allow conda to pick the right binary per platform
- **Do** test that the API behavior is consistent after migration (not just that install succeeds)
