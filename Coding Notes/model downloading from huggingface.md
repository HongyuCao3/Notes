## 📘 Downloading LLaMA Models from Hugging Face (Linux Server Guide)

### 1. Prerequisites

* Linux server with sufficient disk space (≥ 20GB recommended)
* Python (conda environment recommended)
* Hugging Face account with approved access to LLaMA

---

### 2. Install Dependencies

```bash
pip install -U huggingface_hub
```

---

### 3. Authenticate with Hugging Face

Generate a token:
👉 [https://huggingface.co/settings/tokens](https://huggingface.co/settings/tokens)

Then login:

```bash
hf auth login
```

* Paste your token
* Token will be saved locally at:

  ```
  ~/.cache/huggingface/token
  ```

---

### 4. ⚠️ Disk Space & Storage Setup (Critical)

Before downloading large models:

```bash
df -h
```

Check:

* `/` (root) → often small
* `/data` → usually large storage

👉 Always download models to large storage (e.g., `/data`)

---

### 5. Configure Hugging Face Cache (Recommended)

Avoid filling root disk:

```bash
export HF_HOME=/data/$USER/hf
export HF_HUB_CACHE=/data/$USER/hf/hub
export HF_XET_CACHE=/data/$USER/hf/xet
export TMPDIR=/data/$USER/hf/tmp
export HF_HUB_DISABLE_XET=1
```

(Optional: add to `~/.bashrc`)

---

### 6. Download Model

```bash
hf download meta-llama/Llama-2-7b-hf \
  --local-dir /data/$USER/models/llama-7b
```

---

### 7. Common Issues

#### ❌ 1. Disk Full

Error:

```
Not enough free disk space
```

Solution:

* Delete partial download
* Move to `/data`

---

#### ❌ 2. Permission Error (403)

Cause:

* No access to model

Fix:

* Request access on Hugging Face model page

---

#### ❌ 3. Slow Download

Optional mirror:

```bash
export HF_ENDPOINT=https://hf-mirror.com
```

---

#### ❌ 4. Download Crash (xet error)

Fix:

```bash
export HF_HUB_DISABLE_XET=1
```

---

### 8. Verify Download

```bash
ls /data/$USER/models/llama-7b
```

Expected files:

* `config.json`
* `pytorch_model-*.bin` or `.safetensors`
* tokenizer files

---

### 9. Load Model in Python

```python
from transformers import AutoTokenizer, AutoModelForCausalLM

model_path = "/data/username/models/llama-7b"

tokenizer = AutoTokenizer.from_pretrained(model_path)
model = AutoModelForCausalLM.from_pretrained(model_path)
```

---

### 10. Best Practices

* Always use `/data` for large models
* Never store models in `/home`
* Backup your HF token securely
* Use environment variables instead of hardcoding paths
* Monitor disk usage regularly:

```bash
df -h
```

---
