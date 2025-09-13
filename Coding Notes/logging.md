# Logging

## logging
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

## loguru

 - basic usage
      ```python
      from loguru import logger

      logger.debug("This is a debug message")
      logger.info("This is an info message")
      logger.warning("This is a warning")
      logger.error("This is an error")
      logger.critical("This is critical")
      ```
 - common features
   - save log to file
      ```python
      logger.add("app.log")
      logger.info("This will be written to app.log")
      ```
   - log rotation
      ```python
      logger.add("app_{time}.log", rotation="500 MB")   # Rotate by size
      logger.add("app_{time}.log", rotation="1 week")   # Rotate by time
      ```
   - compression & retention
      ```python
      logger.add("app_{time}.log", rotation="1 week", compression="zip", retention="10 days")
      ```
   - exception catching
      ```python
      @logger.catch
      def main():
          1 / 0   # Exception will be logged automatically

      main()
      ```
   - custom log format
      ```python
      logger.add("debug.log", format="{time} {level} {message}", level="DEBUG")
      ```