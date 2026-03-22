# Object Oriented Programming

## When to Use a Class

- A function needs **more than ~3 inputs** (group them into a config/dataclass)
- A function **returns more than ~3 values** — classes let you use dot access + autocomplete instead of dict keys
- The code hierarchy/nesting **exceeds 3 levels deep**
- Multiple functions **share state** that needs to persist between calls

## Recommended Packages

- `dataclass` — auto-generates `__init__`, `__repr__`, `__eq__`; great for configs and result containers
  ```python
  from dataclasses import dataclass
  @dataclass
  class TrainConfig:
      lr: float = 1e-3
      epochs: int = 10
      batch_size: int = 32
  ```
- `pydantic` — like dataclass but with **runtime type validation**; ideal for external configs or API inputs

## Responsibility Design: What Goes Where

Place methods in the class that **owns** the data:

| Class | Responsible For |
|-------|----------------|
| `Dataset` | load from file, get entities, filter by time period |
| `RAG` | load/save/generate embeddings, compute similarity, retrieve top-k |
| `Model` | load from checkpoint, inference (with/without RAG) |
| `Evaluator` | compute metrics, save results |

## Tips

- Prefer **composition over inheritance** — attach helper objects as attributes rather than deep class hierarchies
- Use `__repr__` so objects print usefully during debugging
- Keep `__init__` minimal — defer heavy work (file loading, model init) to a separate `setup()` or `load()` method
- `@staticmethod` for utilities that don't need `self`; `@classmethod` for alternative constructors (e.g., `Model.from_config(cfg)`)
