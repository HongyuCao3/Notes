# Logging

## stdlib `logging` — Standard, works everywhere

```python
import logging

logger = logging.getLogger(__name__)   # logger named after module

logging.basicConfig(level=logging.INFO)
logger.info("App started")             # → INFO:mymodule:App started
```

- Use `__name__` so log messages show which module they came from
- Set level: `DEBUG < INFO < WARNING < ERROR < CRITICAL`
- Good for libraries (doesn't impose output format on the caller)

---

## `loguru` — Simpler, richer, recommended for scripts & research

```python
from loguru import logger

logger.debug("debug")
logger.info("info")
logger.warning("warning")
logger.error("error")
```

### Save to file
```python
logger.add("app.log")
```

### Log rotation & cleanup
```python
logger.add("app_{time}.log", rotation="500 MB")          # rotate by size
logger.add("app_{time}.log", rotation="1 week",           # rotate + compress + retain
           compression="zip", retention="10 days")
```

### Custom format
```python
logger.add("debug.log", format="{time} {level} {message}", level="DEBUG")
```

### Auto-catch exceptions
```python
@logger.catch
def main():
    1 / 0   # exception logged automatically with full traceback
```

---

## When to Use Which

| | `logging` | `loguru` |
|---|---|---|
| Libraries / packages | Preferred | Avoid (imposes format on users) |
| Scripts / research code | Fine | Recommended |
| Needs structured logging | With handlers | `logger.add(..., serialize=True)` |
| Exception catching | Manual try/except | `@logger.catch` |
