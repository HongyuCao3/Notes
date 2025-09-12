#　Model Explainability
## Captum

 - Purpose: PyTorch-native interpretability library.

 - Main Features: Attribution methods (Saliency, Integrated Gradients, DeepLIFT, Occlusion, etc.), Layer attribution, Visualization.

 - Basic Usage (Integrated Gradients):
    ```python
    from captum.attr import IntegratedGradients
    import torch

    model = ...  # PyTorch model
    input_tensor = ...  # input tensor

    ig = IntegratedGradients(model)
    attr = ig.attribute(input_tensor, target=0)  # attribution for class 0
    ```
## SHAP

 - Purpose: Model-agnostic interpretability library using Shapley values (game theory).

 - Main Features: Local & global explanations, multiple visualization types, supports tree models, linear models, deep learning, and black-box models.

- Basic Usage (Tree models):
  ```python
  import shap
  import xgboost as xgb

  model = xgb.XGBRegressor().fit(X_train, y_train)
  explainer = shap.TreeExplainer(model)
  shap_values = explainer(X_test)

  shap.summary_plot(shap_values, X_test)    # global importance
  shap.plots.waterfall(shap_values[0])      # single sample
  ```