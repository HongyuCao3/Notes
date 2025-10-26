# Computational Efficiency vs Scalability

This note summarizes the distinction between **computational efficiency** and **scalability**, commonly used in computer science and machine learning literature.

---

## 1. Definitions

### **Computational Efficiency**
- **Definition**: Measures the amount of computational resources required to perform a task under **fixed problem size and hardware**.
- Focuses on **time, memory, and hardware utilization**.
- Typical metrics:
  - Time complexity (e.g., \(O(n^2)\))
  - Space complexity (memory usage)
  - Wall-clock execution time
- Example:
  > An algorithm that reduces training time from 10 hours to 1 hour on a dataset of 10,000 samples has improved computational efficiency.
- [Wikipedia: Computational complexity theory](https://en.wikipedia.org/wiki/Computational_complexity_theory)

### **Scalability**
- **Definition**: Measures how well an algorithm or system **performs as the problem size or resources increase**.
- Evaluates performance under changing conditions:
  - Larger datasets
  - Larger models
  - Distributed or parallel execution
- Focuses on **performance growth trend**, not just absolute efficiency.
- Example:
  > An algorithm that maintains linear growth in training time when dataset size increases 100x demonstrates good scalability.
- [Wikipedia: Scalability](https://en.wikipedia.org/wiki/Scalability)

---

## 2. Relationship

| Aspect                  | Computational Efficiency                  | Scalability                               |
|--------------------------|-------------------------------------------|------------------------------------------|
| Focus                    | Fixed problem size                        | Performance under growing problem size   |
| Metrics                  | Execution time, memory, FLOPs            | Growth rate of execution time, resource usage |
| Example scenario         | Fast on small dataset                     | Handles large datasets efficiently       |
| Notes                    | High efficiency does **not** imply scalability | High scalability does **not** imply high efficiency |

---

## 3. Usage in Papers

- **Computational efficiency**: Compare algorithms **on the same dataset and hardware**.
  > “Our method improves computational efficiency by reducing training time from X hours to Y hours on the same dataset.”

- **Scalability**: Discuss **performance as dataset/model size increases**, or ability to leverage multiple resources.
  > “The proposed algorithm exhibits good scalability: training time grows linearly with dataset size and it efficiently utilizes multiple GPUs.”

- **Both**: When an algorithm is fast and handles large-scale problems.
  > “Our approach achieves both high computational efficiency on small datasets and strong scalability to large datasets.”

---

## 4. Key Takeaway

- **Computational efficiency** = single-run resource usage  
- **Scalability** = performance behavior as problem size or resources grow
