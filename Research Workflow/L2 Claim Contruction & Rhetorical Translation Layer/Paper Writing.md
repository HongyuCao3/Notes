# Research Paper Writing Guide

---

## Title

Combine: **Task** (problem setting) + **Module/Method** (key technical component) + **Objective** (e.g., robustness).
Every word should convey a meaningful insight into the core contribution.

---

## Introduction

### Paragraph 1 — Motivation
- Opening: anchor in a high-impact domain with real-world significance
- Middle: identify concrete technical challenges or gaps
- Closing: state the task or research objective

### Paragraph 2 — Challenges
- State the central challenge (which part of the task needs improvement?)
- Analyze *why* it's hard — under what conditions does current technique fail?
- Motivate the need for a new method

### Paragraph 3 — Prior Work & Limitations
Structure as: **[Related work → Limitation → Key Issue]**, repeated per module.

### Paragraph 4 — Your Contribution
- Introduce core idea / perspective
- Provide high-level theoretical intuition
- Describe specifically designed steps: objective function, training method (1 sentence each)
- Summarize contribution types:
  1. New problem formulation
  2. Technical improvement
  3. Data challenges addressed
  4. Computational benefit (scalable / convergent / efficient)
  5. Application or deployment contribution

```
Our contributions are summarized as follows:
1. We propose ...
2. We develop ...
3. We demonstrate ...
```

---

## Component-wise Writing Guide

### For Technical Components (Non-model)

**A. Purpose** — which specific subtask/challenge does this address? What remains unsolved without it?

**B. Role in Pipeline** — input/output; how it mitigates a specific failure mode of existing approaches.

**C. Step-by-step Implementation**
1. Construct intermediate structures (clusters, graphs, prototypes) from input
2. Estimate reliability/invariance/stability scores within each structure
3. Convert scores into actionable quantities (weights, constraints, sampling rules)
4. Integrate into the downstream training/optimization process

Use figures to illustrate data flow; add computational remarks if efficiency is improved.

**D. Formal Description (novel operations only)**
Introduce notation and equations only for novel operations. Standard procedures (clustering, cross-entropy, backpropagation) should be described textually or cited — not formalized.

---

### For ML Models

**A. Task Definition** — specify input, output, and learning objective. Clarify whether the model predicts, estimates, decides, or controls.

**B. Modeling Intuition** — why is this architecture appropriate? What assumptions does it encode (smoothness, invariance, structural consistency)? How does the design address the challenges from the Introduction?

**C. Predictive Function**

$$\hat{y} = \mathcal{F}_\theta(\mathbf{x})$$

Avoid expanding standard architectures unless they are modified.

**D. Training Objective (novel parts only)**

$$\mathcal{L} = \sum_i w_i \, \ell(\hat{y}_i, y_i)$$

Standard loss components can be cited, not formalized.

**E. Optimization Strategy** — joint vs. alternating; update frequency of auxiliary quantities; stopping criteria. Focus on training logic, not derivations.

**F. Algorithm (optional)** — pseudocode only if it improves clarity or reproducibility; show the global training loop, not internal module details.

---

## Experiments

### Design Principles
- Each subsection must directly address one issue raised in the Introduction
- Emphasize findings and *why/when* the method works, not isolated numbers

### Recommended Structure

| Section | Purpose |
|---------|---------|
| Main Results | Validate against strong baselines on core tasks |
| Robustness / Stress Tests | Evaluate under distribution shift, noise, or adversarial conditions |
| Ablation Studies | Verify necessity and role of each component |
| Mechanism Analysis | Analyze intermediate quantities (weights, scores) to explain gains |
| Efficiency & Scalability | (if applicable) cost, memory, runtime |
| Hyperparameter Sensitivity | Demonstrate stability, not fine-tuning |

### Writing Each Result
1. State a clear empirical finding
2. Support with quantitative results (table or figure)
3. Give a mechanistic explanation linking observation to the method
4. Close with a takeaway for the overall contribution

---

## Conclusion

1. Background recap — why is this topic important?
2. Research goal — what did you aim to address?
3. Gap overcome — what prior limitations did you resolve?
4. Paper summary + contributions list
5. Key findings from results
6. Experimental insights
7. Theoretical implications
8. Practical implications
9. Limitations and future work
