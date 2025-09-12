# Serialization & Compression
## compress_pickle

- Purpose: Serialize Python objects with optional compression (smaller file size, faster I/O).

 - Typical Use Cases: Save large Python objects (like dictionaries, NumPy arrays, ML models).

 - Basic Usage:
    ```python
    import compress_pickle

    # Save object with compression
    data = {"a": [1, 2, 3], "b": "hello"}
    compress_pickle.dump(data, "data.pbz2")

    # Load object
    loaded = compress_pickle.load("data.pbz2")
    ```

 - Supported compression algorithms: bz2, gzip, lzma, zstandard, etc.