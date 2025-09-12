# Data Structures & Algorithms
## bisect

 - Purpose: Maintain sorted lists and perform binary search efficiently.

 - Typical Use Cases: Insert into sorted lists, find insertion positions, implement ordered collections.

-  Basic Usage:

      ```python
      import bisect
      arr = [1, 3, 4, 7]

      # Find insertion point
      pos = bisect.bisect(arr, 5)   # → 3

      # Insert while keeping list sorted
      bisect.insort(arr, 5)         # arr → [1, 3, 4, 5, 7]
      ```

 - Key functions:

   - bisect_left(list, x) → leftmost position

   - bisect_right(list, x) / bisect(list, x) → rightmost position

   - insort_left(list, x), insort_right(list, x)