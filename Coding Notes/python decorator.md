
---

# 🧠 **Python Decorators – Quick Recall Notes**

## 1. What a Decorator *is*

* A decorator is **a function that takes another function or class and returns a modified version of it**.
* Purpose: **inject behavior without changing the original implementation**.
* Formally, a decorator is a **higher-order function**:

  ```python
  decorated = decorator(original)
  ```

  Using `@decorator` is just syntactic sugar.

### Intuition

> Think of decorators as “wrappers” that add cross-cutting features (logging, timing, config injection) while keeping the core logic clean.

---

# 2. Core Use Cases in Research Engineering

Decorators shine in three scenarios:

### **(1) Runtime Behavior Injection**

* Logging
* Timing
* Automatic exception handling
* Autocasting / no-grad inference

### **(2) Configuration and Experiment Control**

* Hydra config injection
* Automatic experiment directory creation
* Seed fixing
* Caching expensive computations

### **(3) Modular Architecture**

* Model registry
* Dataset registry
* Pipeline stage registration

---

# 3. Essential Built-in & Standard-Library Decorators

### ⭐ `@functools.lru_cache(maxsize=N)`

Caches function outputs for performance.
Ideal for: tokenizer loading, dataset metadata, slow preprocessing.

### ⭐ `@functools.cache`

Unlimited cache (Python 3.9+).

### ⭐ `@property` / `@cached_property`

Lazy computation of attributes.

### ⭐ `@dataclasses.dataclass`

Auto-generates `__init__`, `__repr__`, `__eq__`, etc.

### ⭐ `@contextlib.contextmanager`

Turns a function into a context manager; ideal for resource control.

### ⭐ `@functools.wraps(func)`

Must-use when writing custom decorators; preserves original function metadata.

---

# 4. PyTorch Decorators You Will Use Constantly

### ⭐ `@torch.no_grad()`

Disable gradient tracking → inference mode, saves memory + speed.

### ⭐ `@torch.inference_mode()`

More strict & faster inference; recommended over `no_grad()`.

### ⭐ `@torch.cuda.amp.autocast()`

Automatic mixed precision (AMP) for faster training/inference.

### ⭐ `@torch.compile()`

(For PyTorch 2.x) JIT-style optimization for model forward passes.

---

# 5. Hydra / OmegaConf Decorators

### ⭐ `@hydra.main(config_path, config_name)`

Main entry point for config-driven experiments.
Auto-creates `cfg: DictConfig`.

### ⭐ `hydra.utils.instantiate(cfg)`

(Not syntactically a decorator, but often used *like* one.)
Auto-instantiates classes/functions from config dictionaries.

Useful for:

```yaml
model:
  _target_: src.models.MLP
  input_dim: 128
```

---

# 6. Loguru Decorator

### ⭐ `@logger.catch`

Automatic exception handling with full traceback + optional file logging.

Ideal for:

* training loop entry
* evaluation entry
* pipeline components

---

# 7. Third-Party Highly Practical Decorators

### ⭐ `@retry` (from **tenacity**)

Auto-retry unstable operations (e.g., dataset download, API calls).

### ⭐ `@ray.remote`

Parallel task execution; important for large-scale hyperparameter search.

### ⭐ `@numba.jit`

JIT optimization for CPU/GPU numerical code.

### ⭐ `@click.command`

Create clean command-line interfaces.

### ⭐ `@validate_arguments` (Pydantic)

Runtime argument type checking.

---

# 8. Research-Oriented Custom Decorators (Most Useful in Practice)

These are typically handcrafted inside your research codebase:

### 🔹 `@timeit`

Logs execution time for profiling training steps or dataset preprocessing.

### 🔹 `@set_seed`

Automatically sets random seeds across `torch`, `numpy`, and `random`.

### 🔹 `@track_experiment`

Automatically creates a unique experiment directory and attaches Loguru handler.

### 🔹 `@auto_save_config`

Saves Hydra config to the experiment directory for reproducibility.

### 🔹 `@register_model(name)`

Creates a registry for plug-and-play model construction.

---

# 9. A Typical Real-World Stack (Combining Multiple Decorators)

```python
@hydra.main(config_path="conf", config_name="train")
@logger.catch
@set_seed(42)
@track_experiment
@auto_save_config
@timeit
def train(cfg):
    ...
```

This produces a clean training entry while automatically handling:

* Hydra config loading
* Logging
* Seed fixing
* Experiment directory management
* Config saving
* Timing/reporting

**The training logic remains pure and uncluttered.**

---

# 10. Mental Model to Remember

Decorators help separate:

| **Algorithm Logic** | **Engineering Logic**            |
| ------------------- | -------------------------------- |
| model, loss, optim  | logs, config, timing, robustness |

> Use decorators whenever you need *cross-cutting functionality* that should not pollute your core research code.

---
