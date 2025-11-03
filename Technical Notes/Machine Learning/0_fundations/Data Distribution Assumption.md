# Common Data Distribution Assumptions in Machine Learning

Machine learning methods rely on different assumptions about the underlying data distribution.  
The **strength of the assumption** determines both the **simplicity of the method** and its **robustness to real-world variability**.  
This note summarizes the most common assumptions, their mathematical forms, intuitive meanings, and research extensions when the assumptions are violated.

---

## 1. IID Assumption (Independent and Identically Distributed)

**Formal Definition:**
$$
(x_i, y_i) \sim P(X, Y), \quad (x_i, y_i) \perp (x_j, y_j) \text{ for } i \ne j
$$

**Meaning:**  
All samples are drawn independently from the same distribution.

**Intuition:**  
Each training example is an independent snapshot of the same data-generating process.

**Typical Methods:**  
Classical supervised learning, generalization theory (PAC, VC bounds)

**When Violated →**  
Non-IID learning, domain shift, temporal dependency

---

## 2. Covariate Shift

**Assumption:**
$$
P_{\text{train}}(Y|X) = P_{\text{test}}(Y|X), \quad P_{\text{train}}(X) \ne P_{\text{test}}(X)
$$

**Meaning:**  
Input distribution changes, but the conditional label mechanism remains the same.

**Intuition:**  
The appearance of data varies across domains, while the underlying rule is stable.

**Typical Methods:**  
Importance weighting, domain adaptation

**When Violated →**  
Label shift, concept drift

---

## 3. Label Shift

**Assumption:**
$$
P_{\text{train}}(X|Y) = P_{\text{test}}(X|Y), \quad P_{\text{train}}(Y) \ne P_{\text{test}}(Y)
$$

**Meaning:**  
Feature generation is unchanged, but the class prior differs.

**Intuition:**  
Class balance changes between datasets (e.g., disease prevalence differences).

**Typical Methods:**  
Reweighting via estimated class priors, EM-based estimation

---

## 4. Concept Drift

**Assumption:**
$$
P_{\text{train}}(Y|X) \ne P_{\text{test}}(Y|X)
$$

**Meaning:**  
The underlying concept or labeling rule evolves over time or environments.

**Intuition:**  
Real-world mechanisms change (e.g., user behavior, policies).

**Typical Methods:**  
Online learning, continual learning, drift detection + adaptation

---

## 5. Stationarity Assumption

**Assumption:**
$$
P_t(X, Y) = P_{t'}(X, Y), \quad \forall t, t'
$$

**Meaning:**  
The joint distribution does not change over time.

**Intuition:**  
Statistical properties (mean, variance) remain constant.

**Typical Methods:**  
ARIMA, RNN, Transformer-based forecasting

**When Violated →**  
Non-stationary or adaptive time-series modeling

---

## 6. Exchangeability

**Assumption:**
$$
P(x_1, \dots, x_n) = P(x_{\pi(1)}, \dots, x_{\pi(n)}), \quad \forall \text{ permutation } \pi
$$

**Meaning:**  
The order of samples does not affect the joint distribution.

**Intuition:**  
Data can be treated as an unordered set.

**Typical Methods:**  
Set-based models, graph learning

**When Violated →**  
Sequential modeling, causal order learning

---

## 7. Locality (Smoothness) Assumption

**Assumption:**
If two inputs are close, their outputs should be similar:
$$
\|x_i - x_j\| \text{ small } \Rightarrow |f(x_i) - f(x_j)| \text{ small}
$$

**Meaning:**  
Local neighborhoods in input space correspond to similar labels.

**Intuition:**  
Smoothness of the function mapping; small input perturbations should not change predictions drastically.

**Typical Methods:**  
KNN, kernel methods, CNNs

**When Violated →**  
Adversarial examples, domain generalization

---

## 8. Manifold Assumption

**Assumption:**
$$
X \subset \mathcal{M}, \quad \dim(\mathcal{M}) \ll \dim(\mathcal{X})
$$

**Meaning:**  
High-dimensional data lie on a low-dimensional manifold.

**Intuition:**  
Only a few directions capture meaningful variation in data.

**Typical Methods:**  
Autoencoders, VAEs, diffusion models, manifold regularization

---

## 9. Conditional Independence Assumption

**Assumption:**
$$
X_i \perp X_j \mid Z
$$

**Meaning:**  
Given a latent variable (e.g., cause), observed variables are conditionally independent.

**Intuition:**  
Dependencies arise through hidden factors.

**Typical Methods:**  
Causal discovery, Bayesian networks, graphical models, HMMs

---

## 10. Domain Invariance Assumption

**Assumption:**
There exists a mapping $\phi(X)$ such that:
$$
P_{\text{env}}(Y | \phi(X)) \text{ is invariant across environments } e
$$

**Meaning:**  
Despite different domain distributions, a stable representation exists for prediction.

**Intuition:**  
The model learns causal or invariant features shared by all environments.

**Typical Methods:**  
IRM, VREx, CORAL, DANN, domain generalization frameworks

**When Violated →**  
Partial invariance, causal feature shift

---

## Summary Table

| Assumption | Mathematical Form | Intuition | Typical Methods | When Violated → |
|-------------|-------------------|------------|------------------|-----------------|
| IID | $P(X, Y)$ same & independent | Identical, independent samples | Classical supervised learning | Non-IID, shift |
| Covariate Shift | $P(X)$ changes, $P(Y\|X)$ same | Input changes, rule fixed | Domain adaptation | Concept drift |
| Label Shift | $P(Y)$ changes, $P(X\|Y)$ same | Class prior shift | Reweighting | Joint shift |
| Concept Drift | $P(Y\|X)$ changes | Mechanism change | Online learning | Causal learning |
| Stationarity | $P_t = P_{t'}$ | Time-invariant process | Forecasting | Nonstationary |
| Exchangeability | Permutation invariant | Unordered samples | Set / Graph learning | Sequence modeling |
| Locality | Nearby inputs → nearby outputs | Smooth mapping | KNN, CNN | Adversarial |
| Manifold | Low-dim manifold | Structured data space | Autoencoder | Disentangled rep. |
| Cond. Independence | $X_i \perp X_j\|Z$ | Hidden cause explains dependence | Graphical models | Latent discovery |
| Domain Invariance | $P(Y\|\phi(X))$ stable across envs | Causal representation | IRM, DG | Partial invariance |

---

## Key Takeaway

> In machine learning, every method implicitly assumes something about the data distribution.  
> **Stronger assumptions** simplify modeling but limit generality,  
> while **weaker assumptions** lead to more complex, yet more robust and insightful methods.  
> Scientific innovation often comes from **challenging or relaxing existing assumptions** to handle real-world data variability.

---
