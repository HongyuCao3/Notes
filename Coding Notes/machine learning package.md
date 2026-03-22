# CatBoost vs RandomForest

## Core Difference

- **CatBoost** → Gradient Boosting: trees built **sequentially**, each correcting the previous
- **RandomForest** → Bagging: trees built **in parallel** on random subsets, results averaged

## Comparison

| Aspect | CatBoostRegressor | RandomForestRegressor |
|--------|-------------------|-----------------------|
| Training | Sequential (slow, but GPU helps) | Parallel (fast by default) |
| Categorical features | Native support — no encoding needed | Must encode manually |
| Overfitting control | Ordered Boosting + regularization | Random subsampling of features/samples |
| Prediction speed | Fast (shallow symmetric trees) | Slower with many deep trees |
| Accuracy | Higher on complex tasks | Strong baseline, often slightly lower |
| Interpretability | Built-in SHAP values | Feature importance, weaker |
| Best for | High-dim, categorical-heavy, competitions | Quick baseline, simple tasks |

## Key Takeaways

- Use **CatBoost** when accuracy matters and you have categorical features — it handles them natively and usually wins on leaderboards
- Use **RandomForest** as a fast, reliable **baseline** — parallelizable and hard to overfit badly
- Both are tree ensembles → both support feature importance out of the box

## Minimal Code

```python
# CatBoost
from catboost import CatBoostRegressor
model = CatBoostRegressor(iterations=500, depth=6, learning_rate=0.1, verbose=100)
model.fit(X_train, y_train, eval_set=(X_val, y_val), cat_features=cat_cols)

# RandomForest
from sklearn.ensemble import RandomForestRegressor
model = RandomForestRegressor(n_estimators=300, max_depth=None, n_jobs=-1, random_state=42)
model.fit(X_train, y_train)
```
