# Python Decorators

## What Is a Decorator

- A function that **wraps another function** to inject behavior without changing its implementation
- `@decorator` is syntactic sugar for `func = decorator(func)`
- Core use: separate **engineering concerns** (logging, timing, config) from **algorithm logic**

---

## Standard Library Decorators

| Decorator | Purpose |
|-----------|---------|
| `@functools.lru_cache(maxsize=N)` | Cache return values — great for slow repeated calls |
| `@functools.cache` | Unlimited cache (Python 3.9+) |
| `@property` | Compute attribute lazily on access |
| `@cached_property` | Compute once, cache result on instance |
| `@dataclasses.dataclass` | Auto-generate `__init__`, `__repr__`, `__eq__` |
| `@staticmethod` / `@classmethod` | No `self` / alternative constructor |
| `@functools.wraps(func)` | Preserve original function name/docstring in custom decorators |

---

## PyTorch Decorators

| Decorator | Purpose |
|-----------|---------|
| `@torch.no_grad()` | Disable gradient tracking for inference |
| `@torch.inference_mode()` | Stricter + faster inference (prefer over `no_grad`) |
| `@torch.cuda.amp.autocast()` | Auto mixed precision (FP16/BF16) for speed |
| `@torch.compile` | JIT optimize model (PyTorch 2.x) |

---

## Research / Experiment Decorators

| Decorator | Purpose |
|-----------|---------|
| `@hydra.main(config_path, config_name)` | Entry point for config-driven experiments |
| `@logger.catch` (loguru) | Auto-log exceptions with full traceback |
| `@retry` (tenacity) | Retry on failure — good for API calls or downloads |
| `@validate_call` (pydantic) | Runtime argument type checking |

---

## Custom Research Decorators (Common Patterns)

```python
import functools, time

# Timing
def timeit(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        t0 = time.perf_counter()
        result = func(*args, **kwargs)
        print(f"{func.__name__} took {time.perf_counter() - t0:.2f}s")
        return result
    return wrapper

# Seed fixing
def set_seed(seed):
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            import random, numpy as np, torch
            random.seed(seed); np.random.seed(seed); torch.manual_seed(seed)
            return func(*args, **kwargs)
        return wrapper
    return decorator
```

---

## Real-World Stack (Research Training Entry)

```python
@hydra.main(config_path="conf", config_name="train")
@logger.catch
@set_seed(42)
@timeit
def train(cfg):
    ...
```

This single function handles: config loading, exception logging, reproducibility, and timing — keeping training logic clean.

---

## Mental Model

> Decorators = inject **how** without changing **what**. Use them for anything that would otherwise pollute every function (logging, timing, seeding, error handling).
