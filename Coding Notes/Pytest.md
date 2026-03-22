# Pytest

## When to Write Tests

- A class has **more than 3 methods** — pytest keeps them organized
- You've verified a function works in `if __name__ == "__main__"` — **move that code to a test file**
- Any function with non-trivial logic or edge cases worth guarding against regression

## Basic Structure

```python
# test_mymodule.py
def test_addition():
    assert 1 + 1 == 2

def test_raises():
    with pytest.raises(ValueError):
        int("not a number")
```

Run with: `pytest` or `pytest -v` (verbose) or `pytest -k "test_name"` (filter)

## Fixtures — Shared Setup

```python
import pytest

@pytest.fixture
def sample_data():
    return {"a": 1, "b": 2}

def test_keys(sample_data):
    assert "a" in sample_data  # fixture injected automatically
```

- Use `scope="module"` or `scope="session"` for expensive setup (e.g., loading a model once)

## Parametrize — Test Multiple Inputs

```python
@pytest.mark.parametrize("x,expected", [(2, 4), (3, 9), (4, 16)])
def test_square(x, expected):
    assert x ** 2 == expected
```

## Marks — Skip or Flag Tests

```python
@pytest.mark.skip(reason="not implemented yet")
def test_todo(): ...

@pytest.mark.skipif(sys.platform == "win32", reason="linux only")
def test_linux_only(): ...
```

## Practical Tips

- Keep test files in a `tests/` folder, mirror the source structure
- Name tests `test_<what_it_does>` — readable without reading the body
- One assertion per test when possible — easier to diagnose failures
- Use `tmp_path` fixture for file I/O tests (pytest provides a temp directory automatically)
- Avoid mocking internals — test behavior, not implementation
