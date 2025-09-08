# Logging

```python
# app.py
import logging

logger = logging.getLogger(__name__)

def main():
    logger.info("应用开始运行")

if __name__ == '__main__':
    logging.basicConfig(level=logging.INFO)
    main()
```
will get a logger named as file name, and output
```shell
INFO:app:应用开始运行
```