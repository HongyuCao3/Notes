# Serialization & Compression

## Quick Decision

| Data Type | Recommended Tool |
|-----------|-----------------|
| Model weights (tensors only) | `safetensors` — safe, fast, no pickle |
| Full PyTorch checkpoint (weights + optimizer + epoch) | `torch.save(state_dict, path)` |
| General Python objects (metrics, configs, arrays) | `compress_pickle` or `joblib` |
| Need fine-grained streaming compression | `python-zstandard` (zstd) |
| Cloud / remote storage | `fsspec` |

---

## safetensors — Recommended for Model Weights

- No pickle → **safe to load from untrusted sources**
- Faster load time than `torch.save` for tensor-heavy checkpoints

```python
from safetensors.torch import save_file, load_file

save_file(model.state_dict(), "model.safetensors")
state_dict = load_file("model.safetensors")
model.load_state_dict(state_dict)
```

Store non-tensor metadata (epoch, hyperparams) separately:
```python
import json
json.dump({"epoch": 12, "lr": 1e-4}, open("meta.json", "w"))
```

---

## torch.save / torch.load — Default PyTorch

```python
torch.save(model.state_dict(), "model.pt")
model.load_state_dict(torch.load("model.pt"))
```

- Flexible: can save any Python object (pickled)
- **Security risk**: never `torch.load` files from untrusted sources — pickle can execute arbitrary code

---

## compress_pickle — Quick Compressed Serialization

```python
import compress_pickle as cp

cp.dump({"metrics": metrics, "arrays": arr}, "artifact.pbz2", compression="zstd")
data = cp.load("artifact.pbz2")
```

- Supports: `bz2`, `gzip`, `lzma`, `zstd`
- Still pickle-based — same security caveat as above

---

## zstd Streaming — Fast + Space Efficient

Best speed/compression tradeoff. Use for large checkpoint archival.

```python
import io, torch, zstandard as zstd

def save_zstd(state_dict, path, level=3):
    buf = io.BytesIO()
    torch.save(state_dict, buf)
    buf.seek(0)
    with open(path, "wb") as f:
        zstd.ZstdCompressor(level=level).stream_writer(f).write(buf.read())

def load_zstd(path):
    with open(path, "rb") as f:
        data = zstd.ZstdDecompressor().stream_reader(f).read()
    return torch.load(io.BytesIO(data))
```

- Compression levels 1–5 for checkpoints (favor speed); higher for archival

---

## PyTorch Lightning: Compress Checkpoint via Callback

```python
import shutil, zstandard as zstd
from pytorch_lightning import Callback

class CompressCheckpointCallback(Callback):
    def __init__(self, level=3):
        self.level = level

    def on_train_epoch_end(self, trainer, pl_module):
        # Hook into Lightning's checkpoint writing
        pass  # see on_save_checkpoint for pre-save hook

    # After save: compress .ckpt → .ckpt.zst, remove original
```

---

## Practical Recipe

1. Save weights as `model.safetensors` + metadata as `meta.json`
2. For full checkpoints (optimizer state, epoch), use Lightning's `ModelCheckpoint` + a compress callback
3. Put compression config (algorithm, level) into Hydra so every run logs it
4. For cloud: compress locally, then upload via `fsspec` to `s3://` or `gs://`

---

## Security Note

`torch.load`, `compress_pickle.load`, `joblib.load` — all use pickle and **can execute arbitrary code**. Only load files you trust. Use `safetensors` when sharing model weights publicly.
