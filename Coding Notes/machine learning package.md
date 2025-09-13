# 📘 CatBoostRegressor vs RandomForestRegressor

## 1. Overview
Both **CatBoostRegressor** and **RandomForestRegressor** are tree-based machine learning algorithms, but they follow different principles:

- **CatBoostRegressor** → Gradient Boosting framework  
- **RandomForestRegressor** → Bagging (Random Forests)

---

## 2. Comparison Table

| Aspect | **CatBoostRegressor** | **RandomForestRegressor** |
|--------|------------------------|----------------------------|
| **Core Idea** | Gradient Boosting: sequentially fit new trees to correct residuals of previous trees. | Bagging: train many independent trees on bootstrapped samples and average results. |
| **Tree Structure** | Symmetric (Oblivious) Trees → efficient, balanced, easy to deploy. | Standard Decision Trees → flexible, no structural constraint. |
| **Training** | Sequential (boosting); each tree depends on previous trees. | Parallel (bagging); trees are independent and trained simultaneously. |
| **Categorical Features** | Native support (`cat_features`), no need for one-hot/label encoding. | No native support; must preprocess categorical features manually. |
| **Bias-Variance** | Low bias, high variance, but boosting reduces bias significantly. | High variance, bagging reduces variance but bias may remain larger. |
| **Overfitting Control** | Ordered Boosting + regularization. | Randomness in feature and sample selection reduces overfitting. |
| **Training Speed** | Slower (sequential), but GPU acceleration makes it competitive. | Faster (parallelizable by default). |
| **Prediction Speed** | Fast (trees are shallow and symmetric). | Slower when many deep trees are used. |
| **Interpretability** | Built-in feature importance & SHAP values. | Feature importance available, but weaker interpretability compared to SHAP. |
| **Best Use Cases** | High-dimensional data, categorical-rich datasets, need for high accuracy (finance, healthcare, recommendation). | Moderate datasets, simpler tasks, strong baseline model. |

---

## 3. Key Takeaways
- **CatBoostRegressor** is ideal for datasets with categorical features and high-dimensional tasks where accuracy is critical.  
- **RandomForestRegressor** is simple, robust, parallelizable, and serves well as a strong baseline.  

---

## 4. Code Examples

### CatBoost Regressor
```python
from catboost import CatBoostRegressor, Pool
from sklearn.model_selection import train_test_split
from sklearn.datasets import fetch_california_housing

# Load dataset
X, y = fetch_california_housing(return_X_y=True, as_frame=True)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Initialize model
cat_model = CatBoostRegressor(
    iterations=500, depth=6, learning_rate=0.1,
    loss_function='RMSE', verbose=100, random_seed=42
)

# Train
cat_model.fit(X_train, y_train, eval_set=(X_test, y_test))
