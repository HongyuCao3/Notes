# Best Practices for Notation in Machine Learning and Deep Learning Papers

This document provides a **community-aligned, paper-oriented notation guideline** for machine learning (ML) and deep learning (DL) research. The goal is to **minimize reader confusion**, **avoid subscript explosion**, and **maintain semantic consistency** across models, losses, and optimization procedures.

---

## 1. Core Design Principles

### 1.1 One Semantic Concept → One Symbol

Each mathematical symbol should correspond to **exactly one semantic role** throughout the paper.

* Prefer different letters over overloaded subscripts
* Do not encode semantics in subscripts

**Bad:**
[ \lambda_{cls}, \lambda_{reg}, \lambda_{aux} ]

**Good:**
[ \mathcal{L} = \sum_{k=1}^K \lambda_k \mathcal{L}_k ]

---

### 1.2 Subscripts Are for Indices, Not Meaning

Valid subscripts:

* Sample index: $i, j$
* Layer index: $l$
* Time step: $t$

Avoid semantic subscripts such as:

* $\lambda_{adv}$
* $\theta_{shared}$

---

### 1.3 Do Not Redefine Community-Conventional Symbols

Reusing a symbol with a conflicting meaning introduces **implicit cognitive load** for reviewers.

Example:

* $\lambda$ → regularization / loss weight (do **not** use as learning rate)
* $\beta_1, \beta_2$ → Adam parameters only

---

## 2. Model Parameters

### 2.1 Global Model Parameters

| Concept                 | Recommended Symbol |
| ----------------------- | ------------------ |
| All model parameters    | $\theta$         |
| Parameters of layer $l$ | $\theta^{(l)}$   |

---

### 2.2 Layer-wise Parameters

| Concept       | Symbol      |
| ------------- | ----------- |
| Weight matrix | $W^{(l)}$ |
| Bias vector   | $b^{(l)}$ |

Example:
$$f(x; \theta) = W^{(L)} \sigma( \cdots W^{(1)} x + b^{(1)} ) + b^{(L)}$$

---

### 2.3 Auxiliary / Learnable Scalars

| Usage                 | Symbol     |
| --------------------- | ---------- |
| Scaling / temperature | $\tau$   |
| Gating coefficient    | $\alpha$ |
| Mixture weights       | $\pi$    |

---

## 3. Loss Functions and Objectives

### 3.1 Loss Terms

| Concept              | Symbol            |
| -------------------- | ----------------- |
| Total loss           | $\mathcal{L}$   |
| Individual loss term | $\mathcal{L}_k$ |

---

### 3.2 Loss Weights (Critical Section)

| Usage                 | Symbol         |
| --------------------- | -------------- |
| Loss weighting        | $\lambda$    |
| Multiple loss weights | $\lambda_k$  |
| Time-dependent weight | $\lambda(t)$ |

Recommended form:
$$
\mathcal{L} = \sum_{k=1}^K \lambda_k \mathcal{L}_k
$$

---

### 3.3 Regularization

| Type                   | Symbol      |
| ---------------------- | ----------- |
| L1 / L2 regularization | $\lambda$ |
| Auxiliary penalty      | $\gamma$  |

---

## 4. Optimization Notation

| Concept           | Symbol               | Notes         |
| ----------------- | -------------------- | ------------- |
| Learning rate     | $\eta$             | DL standard   |
| Momentum          | $\mu$              | SGD           |
| Adam coefficients | $\beta_1, \beta_2$ | Fixed meaning |
| Iteration         | $t$                | Step index    |

Update rule example:
$$\theta_{t+1} = \theta_t - \eta , \nabla_{\theta} \mathcal{L}$$

---

## 5. Thresholds, Margins, and Temperatures

| Concept            | Symbol   |
| ------------------ | -------- |
| Decision threshold | $\tau$ |
| Margin             | $m$    |
| Logit temperature  | $\tau$ |
| Clipping value     | $c$   |

---

## 6. Probabilities and Uncertainty

| Concept      | Symbol       |
| ------------ | ------------ |
| Probability  | $p$        |
| Logits       | $z$        |
| Variance     | $\sigma^2$ |
| Distribution | $p(x)$     |

---

## 7. Vector and Matrix Conventions

### 7.1 Typography

| Object | Convention                     |
| ------ | ------------------------------ |
| Scalar | lowercase italic: $a$        |
| Vector | bold lowercase: $\mathbf{x}$ |
| Matrix | bold uppercase: $\mathbf{W}$ |
| Set    | calligraphic: $\mathcal{S}$  |

---

### 7.2 Vectors over Subscripts

Instead of:
[ \lambda_1, \lambda_2, \dots, \lambda_K ]

Use:
[ \boldsymbol{\lambda} \in \mathbb{R}^K ]

---

## 8. Avoiding Subscript Explosion

### 8.1 Index Sets

$$\mathcal{L} = \sum_{\mathcal{L}_k \in \mathcal{S}} \lambda_k \mathcal{L}_k$$

---

### 8.2 Functional Dependence Instead of Indexing

$$\lambda = f(t) \quad \text{instead of} \quad \lambda_t$$

---

## 9. Quick Reference Table

```
θ      : model parameters
W, b   : layer weights and biases
ℒ      : total loss
ℒ_k    : k-th loss term
λ_k    : loss weight
η      : learning rate
μ      : momentum
τ      : threshold / temperature
m      : margin
π      : mixture weights
σ²     : variance
```

---

## 10. Final Recommendation

If a symbol requires a long verbal explanation, the notation is likely over-engineered. Prefer **semantic clarity over mathematical compression**.
