# Model Explainability

## Why It Matters

- **Debug** models — catch shortcut learning, spurious correlations
- **Validate** that the model uses domain-relevant features (not artifacts)
- **Communicate** results to stakeholders or for paper interpretability sections
- Required in high-stakes domains: medical, financial, legal

---

## Captum — PyTorch-Native Attribution

- `pip install captum`
- Computes **attribution scores**: how much each input dimension contributed to a prediction
- Works directly on PyTorch computational graphs

### Key Methods

| Method | How It Works | Best For |
|--------|-------------|----------|
| **Saliency** | `∂f/∂x` — gradient of output w.r.t. input | Quick sanity check, noisy |
| **Integrated Gradients (IG)** | Integrates gradients along path from baseline to input | Most reliable; use in papers |
| **DeepLIFT** | Propagates contribution scores vs. a baseline | Handles gradient saturation |
| **Occlusion** | Masks parts of input, measures output change | Gradient-free, robust |
| **LayerGradCam** | Attribution on intermediate CNN layers | Feature map / attention analysis |

### Usage Pattern

```python
from captum.attr import IntegratedGradients

model.eval()
ig = IntegratedGradients(model)
attr = ig.attribute(
    input_tensor,
    baselines=torch.zeros_like(input_tensor),
    target=class_idx
)
# attr has same shape as input — positive = contributed positively to prediction
```

### Typical Workflow
1. Train model → save checkpoint
2. Load in eval mode
3. Run attribution on val/test samples
4. Visualize (heatmaps for images, token scores for NLP)

---

## SHAP — Model-Agnostic, Theory-Grounded

- `pip install shap`
- Based on **Shapley values** (cooperative game theory): each feature gets its fair average marginal contribution
- Decomposes prediction: `f(x) = baseline + Σ φᵢ`

### Explainer Types

| Explainer | Best For |
|-----------|----------|
| `TreeExplainer` | XGBoost, LightGBM, CatBoost, RandomForest — **exact, fast** |
| `DeepExplainer` | PyTorch / TensorFlow neural nets — approximate |
| `KernelExplainer` | Any black-box model — slowest, most general |

### Usage Pattern

```python
import shap

explainer = shap.TreeExplainer(model)
shap_values = explainer(X_test)

shap.summary_plot(shap_values, X_test)      # global feature importance
shap.waterfall_plot(shap_values[0])          # single sample explanation
```

---

## Captum vs SHAP — When to Use Which

| | Captum | SHAP |
|--|--------|------|
| Framework | PyTorch-native | Model-agnostic |
| Theory | Gradients / backprop | Shapley values (game theory) |
| Best for | Deep learning, CNNs, Transformers | Tabular ML, tree ensembles |
| Guarantees | Some (IG satisfies completeness) | Strong theoretical guarantees |
| Stakeholder-friendly | Less so | Yes (intuitive feature scores) |

**Use Captum** for deep learning research papers — layer attribution, attention analysis, CNN heatmaps.

**Use SHAP** for tabular data, tree models, and any time you need interpretable feature rankings for stakeholders.
