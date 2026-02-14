# Model Explainability

Model explainability (or interpretability) refers to a family of techniques that aim to make machine learning models—especially deep neural networks—more transparent by identifying which inputs, features, or internal components contribute to specific predictions. In research and production settings, explainability serves multiple roles:

* **Model debugging** (detecting spurious correlations, shortcut learning)
* **Feature validation** (confirming domain-relevant signals are used)
* **Trust and transparency** (e.g., medical, financial, legal applications)
* **Ablation and interpretability experiments in papers**
* **Regulatory compliance and risk assessment**

Below are two widely used libraries: **Captum** (PyTorch-native) and **SHAP** (model-agnostic, Shapley-based).

---

# Captum

## 1. What Captum Actually Does

Captum is a **PyTorch-native model interpretability library** that computes *attribution scores* for inputs, intermediate layers, or neurons in neural networks.

In formal terms, most Captum methods compute:

[
\text{Attribution} = \frac{\partial f(x)}{\partial x}
\quad \text{or a related functional approximation}
]

where:

* ( f(x) ) is the model output (e.g., logit for class k)
* ( x ) is the input tensor
* Attribution measures the contribution of each input dimension to the output

Captum focuses primarily on:

* **Gradient-based attribution**
* **Path-based attribution**
* **Perturbation-based attribution**
* **Layer / neuron-level attribution**

It is designed specifically for **PyTorch computational graphs** and leverages automatic differentiation.

---

## 2. Core Attribution Methods

### (1) Saliency

Computes:
[
\frac{\partial f(x)}{\partial x}
]

Interpretation:

* Measures local sensitivity
* Highlights pixels/features where small changes strongly affect output

Use case:

* Quick sanity check for CNN attention regions
* Not robust (can be noisy)

---

### (2) Integrated Gradients (IG)

Computes:
[
\text{IG}(x) = (x - x') \int_{0}^{1} \frac{\partial f(x' + \alpha(x - x'))}{\partial x} d\alpha
]

where:

* ( x' ) is a baseline (e.g., zero image)

Key properties:

* Satisfies **completeness axiom**
* More stable than plain gradients

Use in papers:

* Feature importance comparison
* Demonstrating model reliance on specific input regions
* Validating domain-relevant signals

---

### (3) DeepLIFT

Compares activation differences relative to a baseline and propagates contribution scores backward.

Strength:

* Handles gradient saturation better than pure gradients

---

### (4) Occlusion

Perturbation-based:

* Systematically masks parts of the input
* Measures change in output

Useful when:

* Gradients are unreliable
* Interpreting tabular or vision models

---

### (5) Layer Attribution

Captum supports:

* LayerIntegratedGradients
* LayerGradCam
* Neuron attribution

Use case:

* Understanding intermediate feature representations
* Analyzing attention maps
* CNN feature map visualization
* Transformer head analysis

---

## 3. Where Captum Is Used in Research

Captum is typically used in:

### (A) Model Validation Section

To show:

* The model attends to clinically relevant regions (medical imaging)
* NLP model focuses on semantically meaningful tokens
* GNN attends to correct substructures

Example phrasing in a paper:

> “We use Integrated Gradients to compute attribution maps and verify that the model predictions rely on domain-relevant features.”

---

### (B) Robustness / Shortcut Learning Analysis

* Detect whether model uses background artifacts
* Identify spurious correlations

---

### (C) Ablation & Attribution Consistency Experiments

Researchers compare:

* Different architectures
* Different training objectives
* Different regularization methods

by measuring:

* Attribution sparsity
* Attribution alignment with ground truth masks

---

## 4. Where Captum Fits in a PyTorch Project

Typical placement:

```
train.py
model.py
evaluate.py
explain.py   <-- Captum here
```

Workflow:

1. Train model
2. Load checkpoint
3. Switch model to eval mode
4. Run attribution on validation/test samples
5. Visualize or log results

Example:

```python
model.eval()
ig = IntegratedGradients(model)

attr = ig.attribute(
    input_tensor,
    baselines=torch.zeros_like(input_tensor),
    target=class_idx
)
```

Captum is typically used:

* After training
* During error analysis
* During experimental evaluation

---

# SHAP

## 1. What SHAP Actually Does

SHAP (SHapley Additive exPlanations) is based on **cooperative game theory**.

It assigns each feature a value:

[
\phi_i = \text{Shapley value of feature } i
]

which represents the average marginal contribution of feature ( i ) across all possible feature subsets.

Mathematically:

[
\phi_i = \sum_{S \subseteq F \setminus {i}}
\frac{|S|!(|F|-|S|-1)!}{|F|!}
\big( f(S \cup {i}) - f(S) \big)
]

Where:

* ( F ) = full feature set
* ( S ) = subset not containing feature i

SHAP provides:

* Theoretically grounded feature importance
* Additive explanation model
* Local + global interpretability

---

## 2. Types of SHAP Explainers

### (1) TreeExplainer

Optimized for:

* XGBoost
* LightGBM
* CatBoost
* Random Forests

Very fast and exact for tree models.

---

### (2) DeepExplainer

For:

* TensorFlow
* PyTorch deep models

Uses approximations of SHAP for neural networks.

---

### (3) KernelExplainer

Model-agnostic.

* Works with any black-box model
* Slower
* Sampling-based approximation

---

## 3. What SHAP Measures Conceptually

SHAP decomposes prediction:

[
f(x) = \phi_0 + \sum_i \phi_i
]

Where:

* ( \phi_0 ) = expected model output
* ( \phi_i ) = contribution of feature i

This allows:

* Per-sample explanation
* Dataset-level importance
* Interaction effect analysis

---

## 4. Where SHAP Is Used in Research

SHAP is commonly used in:

### (A) Tabular ML Papers

* Risk prediction
* Clinical modeling
* Financial forecasting
* Credit scoring

Example usage:

* Ranking most important features
* Demonstrating consistency with domain knowledge
* Interpreting nonlinear interactions

---

### (B) Model Comparison

Researchers compare:

* Feature attribution stability across models
* Impact of feature engineering

---

### (C) Fairness Analysis

* Compare SHAP values across demographic groups
* Identify bias or disproportionate reliance on sensitive features

---

## 5. SHAP in Engineering Pipelines

Typical placement:

```
train_model.py
evaluate_model.py
interpret_model.py   <-- SHAP here
```

Example:

```python
explainer = shap.TreeExplainer(model)
shap_values = explainer(X_test)

shap.summary_plot(shap_values, X_test)
```

Used:

* After model fitting
* During reporting
* For stakeholder presentations

---

# Captum vs SHAP — Conceptual Difference

| Aspect            | Captum               | SHAP                           |
| ----------------- | -------------------- | ------------------------------ |
| Framework         | PyTorch-native       | Model-agnostic                 |
| Theory            | Gradients / backprop | Game theory (Shapley values)   |
| Best for          | Deep learning        | Tree & tabular models          |
| Speed             | Fast (autograd)      | Fast for trees, slow otherwise |
| Guarantees        | Some axioms (IG)     | Strong theoretical guarantees  |
| Local explanation | Yes                  | Yes                            |
| Global importance | Via aggregation      | Built-in                       |

---

# When to Use Which

Use **Captum** if:

* You are working with PyTorch models
* You need layer-level or neuron-level attribution
* You analyze CNN, Transformer, GNN attention
* You publish deep learning research

Use **SHAP** if:

* You work with tabular data
* You use tree ensembles
* You need stakeholder-ready explanations
* You require strong theoretical interpretability guarantees

---

# In a Research Paper: Typical Experimental Section

Explainability experiments often appear as:

### 1. Qualitative Visualization

* Heatmaps on images
* Token importance in NLP
* Feature ranking plots

### 2. Quantitative Metrics

* Attribution faithfulness tests
* Deletion / insertion curves
* Sensitivity-n metrics
* Alignment with ground-truth masks

### 3. Comparative Analysis

* Baseline vs proposed model
* Regularized vs non-regularized model
* Robust vs standard training

---

# Summary

* **Captum**: Gradient/path-based attribution for PyTorch neural networks. Used in deep learning interpretability experiments and debugging.
* **SHAP**: Shapley-value-based model-agnostic framework. Strong theoretical foundation. Common in tabular ML, fairness, and applied research.
* Both are typically used **after model training**, during evaluation and analysis stages.
* In research, they support interpretability claims, robustness analysis, and validation of domain relevance.

