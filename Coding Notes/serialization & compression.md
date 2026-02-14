# Serialization & Compression — integration with PyTorch / PyTorch-Lightning + Hydra

## Summary recommendations (quick)

* **Tensors / model weights:** use **safetensors** (fast, safe, no pickle) for whole-model or `state_dict` storage; fallback to `torch.save(state_dict)` when you need Python objects attached.
* **General Python objects (configs, dicts, metrics):** `compress_pickle` or `joblib.dump(..., compress=...)` are fine — but be explicit about compression algorithm and aware of pickle security.
* **High-performance compression for checkpoints/artifacts:** **zstandard (zstd)** — best speed/compression tradeoff; supported by `python-zstandard` and by `joblib` (via `compress=('zstd', level)`), or by streaming with `zstandard.ZstdCompressor()`.
* **Integration with Lightning:** implement a small post-save compression callback (compress after Lightning writes the checkpoint) or override `on_save_checkpoint`.
* **Hydra config:** supply compression algorithm, level, and artifact path as Hydra config options so experiments are reproducible and auditable.
* **Remote / cloud storage:** combine with `fsspec` (or Lightning’s S3/GS support) so you can compress locally then upload or stream compress to remote.

---

## Libraries and why

* **safetensors**

  * Purpose: store tensor arrays safely and quickly without Python pickle. Ideal for model weights and shared checkpoints where security and read speed matter.
  * Pros: deterministic, secure (no arbitrary code execution), very fast to load for tensor-heavy checkpoints.
  * Cons: stores tensors only (you must separately store Python metadata).

* **torch.save / torch.load**

  * Purpose: default for PyTorch. Stores arbitrary Python objects (pickled).
  * Pros: flexible, native.
  * Cons: uses pickle (unsafe with untrusted files); larger file sizes unless you compress the bytes stream.

* **compress_pickle**

  * Purpose: pickle + optional compression in one API. Works for arbitrary Python objects.
  * Pros: convenient; supports multiple compressors (bz2, gzip, lzma, zstd).
  * Cons: still pickle-based (security); not specialized for tensors.

* **joblib**

  * Purpose: fast serialization for large numpy arrays, supports compression.
  * Pros: optimized for large arrays; `compress=('zlib'|'lz4'|'zstd', level)`; good speed.
  * Cons: semantics differ slightly from pickle; also can execute code when loading pickled objects (caveat like pickle).

* **python-zstandard**

  * Purpose: direct fast zstd compression streaming API — excellent control/performance.
  * Use when you want fast compress/decompress and fine-grained streaming behavior.

* **fsspec**

  * Purpose: unified filesystem interface for local, s3, gcs, azure. Useful for writing compressed files directly to cloud stores.

---

## Practical patterns & examples

### 1) Save `state_dict` using safetensors + metadata (recommended for model weights)

```python
# pip install safetensors
from safetensors.torch import save_file, load_file
import torch

# Save
state_dict = model.state_dict()
# safetensors expects tensors as a mapping: name -> tensor
save_file(state_dict, "model.safetensors")

# Load
loaded = load_file("model.safetensors")
# Convert back to model
model.load_state_dict(loaded)
```

Store non-tensor metadata (hyperparams, epoch) separately as JSON or compressed JSON:

```python
import json, compress_pickle
meta = {"epoch": 12, "lr": 1e-4}
with open("meta.json","w") as f:
    json.dump(meta, f)
# or compress_pickle.dump(meta, "meta.pbz2", compression="zstd")
```

---

### 2) Save `state_dict` with zstd compression (torch + zstandard streaming)

```python
# pip install zstandard
import io, torch, zstandard as zstd

def save_state_dict_zstd(state_dict, path, level=3):
    buf = io.BytesIO()
    torch.save(state_dict, buf)
    buf.seek(0)
    cctx = zstd.ZstdCompressor(level=level)
    with open(path, "wb") as fh:
        with cctx.stream_writer(fh) as compressor:
            compressor.write(buf.read())

def load_state_dict_zstd(path):
    dctx = zstd.ZstdDecompressor()
    with open(path, "rb") as fh:
        decompressed = dctx.stream_reader(fh).read()
    return torch.load(io.BytesIO(decompressed))

# usage
save_state_dict_zstd(model.state_dict(), "model.pt.zst", level=5)
sd = load_state_dict_zstd("model.pt.zst")
model.load_state_dict(sd)
```

---

### 3) Save arbitrary Python objects with `compress_pickle` (quick)

```python
import compress_pickle as cp

data = {"metrics": metrics, "config": cfg, "arrays": numpy_arrays}
cp.dump(data, "artifact.pbz2", compression="zstd")   # choose algorithm explicitly
loaded = cp.load("artifact.pbz2")
```

**Security note:** only load pickled objects you trust.

---

### 4) PyTorch Lightning: compress checkpoint after save (callback)

Use a small Lightning callback that compresses the checkpoint file Lightning just wrote — keeps Lightning checkpointing unchanged and adds compression.

```python
import os, shutil, zstandard as zstd
from pytorch_lightning.callbacks import ModelCheckpoint
from pytorch_lightning import Callback

class CompressCheckpointCallback(Callback):
    def __init__(self, algo="zstd", level=3, keep_uncompressed=False):
        self.algo = algo
        self.level = level
        self.keep_uncompressed = keep_uncompressed

    def on_save_checkpoint(self, trainer, pl_module, checkpoint):
        # Called before lightning writes the checkpoint; do nothing here.
        pass

    def on_checkpoint_save(self, trainer, pl_module, checkpoint_path):
        # Called after checkpoint is written
        if self.algo == "zstd":
            compressed_path = checkpoint_path + ".zst"
            cctx = zstd.ZstdCompressor(level=self.level)
            with open(checkpoint_path, "rb") as src, open(compressed_path, "wb") as dst:
                with cctx.stream_writer(dst) as writer:
                    shutil.copyfileobj(src, writer)
            if not self.keep_uncompressed:
                os.remove(checkpoint_path)
            # Optionally update trainer checkpoint references, upload compressed etc.
```

Add to your trainer:

```python
ckpt_cb = ModelCheckpoint(dirpath="checkpoints", save_top_k=3, monitor="val_loss")
compress_cb = CompressCheckpointCallback(algo="zstd", level=5)
trainer = Trainer(callbacks=[ckpt_cb, compress_cb], ...)
```

If you need Lightning to *load* compressed checkpoints automatically, create a small loader that detects `.zst` and decompresses into a temp file before `torch.load`.

---

### 5) Hydra integration (configs)

Define a Hydra config group `compression`:

```yaml
# config/compression/default.yaml
algorithm: zstd
level: 4
keep_uncompressed: false
artifact_dir: ${hydra:runtime.cwd}/outputs/${now:%Y%m%d_%H%M%S}
```

Use in code:

```python
@hydra.main(config_path="config", config_name="default")
def main(cfg):
    ckpt_cb = ModelCheckpoint(dirpath=cfg.compression.artifact_dir, ...)
    compress_cb = CompressCheckpointCallback(
        algo=cfg.compression.algorithm,
        level=cfg.compression.level,
        keep_uncompressed=cfg.compression.keep_uncompressed,
    )
    trainer = Trainer(callbacks=[ckpt_cb, compress_cb], ...)
```

This keeps compression parameters reproducible in experiment configs.

---

## Tradeoffs & security notes

* **Pickle risk:** `torch.load`, `compress_pickle.load`, and `joblib.load` can execute arbitrary code. Only load files from trusted sources. `safetensors` avoids this risk for tensor data.
* **Compression level vs CPU time:** higher zstd level → smaller file but more CPU/time. Choose a level (1–5) for checkpoints to favor speed; use higher levels for archival.
* **I/O vs CPU:** compressing saves network upload cost (smaller uploads), but if training on I/O-bound cluster, compressing can become CPU-bound. Consider async upload/compress (but you asked for in-turn solutions; if implementing, compress after save in callback).
* **Interoperability:** safetensors + JSON/meta is a robust pattern for sharing weights + provenance; it’s friendly for downstream non-Python consumers.

---

## Minimal practical recipe I use often

1. Save model weights as `model.safetensors`.
2. Save training metadata (epoch, optimizer state, hyperparameters) as `meta.json` or `meta.pbz2` (zstd).
3. Keep a Lightning `ModelCheckpoint` writing best checkpoints; add `CompressCheckpointCallback` to compress full `.ckpt` files for archival if you *must* keep the full checkpoint.
4. Put compression parameters into Hydra so every run logs `algorithm`+`level`.
5. For large datasets or artifacts, write to `fsspec`-backed path (s3://...) after compression.

