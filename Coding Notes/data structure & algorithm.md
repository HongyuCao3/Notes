# Data Structures & Algorithms

## bisect — Binary Search on Sorted Lists

- Maintain sorted order and find insertion positions in O(log n)

```python
import bisect
arr = [1, 3, 4, 7]

bisect.bisect(arr, 5)       # → 3  (rightmost insert position)
bisect.bisect_left(arr, 3)  # → 1  (leftmost: before existing equal elements)
bisect.insort(arr, 5)       # arr → [1, 3, 4, 5, 7]
```

- Use `bisect_left` when you want to find an existing element's index

---

## heapq — Min-Heap / Priority Queue

- Always a **min-heap** — smallest element at `heap[0]`

```python
import heapq
heap = [5, 1, 3]
heapq.heapify(heap)          # in-place: [1, 3, 5]
heapq.heappush(heap, 2)      # push
smallest = heapq.heappop(heap)  # pop min

# Top-k largest
heapq.nlargest(3, data)
heapq.nsmallest(3, data)
```

- For max-heap: negate values (`heappush(heap, -val)`)

---

## collections — Useful Data Containers

### Counter — count frequencies
```python
from collections import Counter
c = Counter("abracadabra")   # Counter({'a': 5, 'b': 2, ...})
c.most_common(3)             # top 3 elements
```

### defaultdict — dict with automatic default
```python
from collections import defaultdict
d = defaultdict(list)
d["key"].append(1)           # no KeyError — auto-creates []
```

### deque — fast append/pop from both ends
```python
from collections import deque
dq = deque([1, 2, 3], maxlen=3)
dq.appendleft(0)   # O(1) left append
dq.popleft()       # O(1) left pop
# maxlen: automatically discards oldest when full — useful for sliding windows
```

### OrderedDict — preserves insertion order (mostly replaced by plain `dict` in Python 3.7+)

---

## itertools — Combinatorics & Iteration

```python
from itertools import combinations, permutations, product, chain

list(combinations([1,2,3], 2))   # [(1,2),(1,3),(2,3)]
list(permutations([1,2,3], 2))   # [(1,2),(1,3),(2,1),...]
list(product([0,1], repeat=3))   # all 3-bit binary strings
list(chain([1,2], [3,4]))        # [1,2,3,4] — flatten iterables
```
