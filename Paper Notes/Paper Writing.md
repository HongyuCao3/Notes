# 📄 Research Paper Writing Guide

---

## 🧩 Introduction

> **Objective**: Establish the background, identify key challenges, highlight gaps in the literature, and present your unique contributions.

### 1. Research Motivation and Importance
- Why is this task/problem **emerging or important**?
- Why is it necessary to address it now? (e.g., due to technical, social, or application-driven reasons)

### 2. Major Challenges
- What are the **key technical or practical challenges**?
- How do these challenges limit current progress?

### 3. Existing Literature and Limitations
- What has prior work done to address this problem?
- **Why are existing methods insufficient**?
  - Poor generalization
  - Sensitivity to distribution shift
  - Scalability issues
- **what's the key issue this paper is going to address**
- <font color =red>composed of Blocks [related works $\Rightarrow$ Limitation $\Rightarrow$ Issue(boldface)]</font>

### 4. Your Unique Perspective and Contributions
- What **novel approach or perspective** do you propose?
- What are the **key contributions** of this paper?

```markdown
Our contributions are summarized as follows:
1. We propose ...
2. We develop ...
3. We demonstrate ...
```

### 5. Summary of the Proposed Solution
- What **framework/model** do you develop?
- What **goals** can it achieve?
- What **technical solutions** are used to achieve these goals?
- What are the **experimental results** and their benefits?

---

## ⚙️ Method

> **Objective**: Present the overall structure and technical components of your approach with clarity and reproducibility.

### 1. Overall Framework

- Use a figure (e.g., `Figure 1`) to visually explain the architecture.
- Provide a high-level description of each component.

```markdown
As shown in Figure X, our framework consists of:
1. Shift-resistant feature set representation;
2. Flatness-aware feature transformation generation;
3. Integrated pre-normalization and post-denormalization.
```

---

### 2. Component-wise Writing Guide

#### 📌 For Technical Components (Non-model)

**A. Purpose of This Section**
- What **specific subtask** does this section solve?

**B. Role in the Overall Framework**
- How does this component **fit into the bigger picture**?
- What challenge does it help mitigate?

**C. Implementation Details**
- What is the **core idea**?
- What are the **main steps** to implement it?
- Include **textual description**, **examples (optional)**, and **figures (optional)**.

```markdown
- Step 1: ...
- Step 2: ...
- Step 3: ...
```

**D. Formal Description**
- Use clear **notations** and **equations** to define the key operation.

```latex
Let $\mathbf{x}$ be the input feature set. The transformed representation is given by:
\[
\mathbf{h} = f_{\text{GNN}}(G(\mathbf{x}))
\]
```

---

#### 🤖 For Machine Learning Models

**A. Task of the Model**
- What is the **input/output/goal** of the model?

**B. Modeling Intuition**
- Why is the model designed this way?
- What assumptions or insights motivate it?

**C. Predictive Function**
- Define the model’s forward function.

```latex
\[
\hat{y} = \mathcal{F}_\theta(\mathbf{x})
\]
```

**D. Loss Function**
- What is the **training objective**?

```latex
\[
\mathcal{L} = \sum_i \ell(\hat{y}_i, y_i)
\]
```

**E. Optimization Strategy**
- How is the model trained? (e.g., gradient descent, inner-outer loop, Bellman equation)

**F. Training Algorithm (Optional)**
- If you use a practical optimization method, provide pseudocode:

```markdown
**Algorithm 1: Model Training**

Input: ...
Output: ...
Repeat:
  1. Sample data ...
  2. Forward pass ...
  3. Compute loss ...
  4. Update parameters ...
Until convergence
```
## Experiments
  - <font color =red>every part address one issue in the introduction</font>
  - ablation study
  - hyper parameter sensitivity analysis

---

## ✅ Conclusion

> **Objective**: Reiterate the importance of your work, summarize findings, and suggest future research.

Use this **sentence-level checklist** to organize your paragraph(s):

1. **Background recap**: Why is this topic important?
2. **Research goal**: What did you aim to address?
3. **Gap in literature**: What previous limitations did you overcome?
4. **Study summary**: What did this paper propose?
5. **Detailed contributions**:

```markdown
Specifically, our contributions include:
- ...
- ...
- ...
```

6. **Key findings**: What do your results suggest?
7. **Experimental insights**: What do your empirical results show?
8. **Theoretical implications**: What do your methods imply theoretically?
9. **Practical implications**: What can practitioners or industry apply from this work?
10. **Limitations and future work**:

```markdown
This study is limited by...
Future research could explore...
```

---
