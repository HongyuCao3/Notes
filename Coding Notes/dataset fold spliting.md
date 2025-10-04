# Scikit-learn Cross-Validation Splitters: KFold, StratifiedKFold, StratifiedGroupKFold

This note summarizes the usage and differences between **KFold**, **StratifiedKFold**, and **StratifiedGroupKFold** in scikit-learn.

---

## 1. `KFold`

- **Description**: Splits dataset into `k` consecutive folds (without shuffling by default).
- **Use case**: General-purpose cross-validation when labels are **not imbalanced** and **group membership is not important**.
- **Key parameters**:
  - `n_splits`: number of folds (default=5).
  - `shuffle`: whether to shuffle before splitting.
  - `random_state`: for reproducibility if `shuffle=True`.

**Example**:
```python
from sklearn.model_selection import KFold

kf = KFold(n_splits=5, shuffle=True, random_state=42)
for train_idx, test_idx in kf.split(X):
    print("Train:", train_idx, "Test:", test_idx)
```
## 2. `StratifiedKFold`

Description: Splits dataset into k folds while preserving the percentage of samples for each class.

Use case: Classification tasks with imbalanced classes.

Key parameters:

Same as KFold (n_splits, shuffle, random_state).

Requirement: Needs labels (y) to enforce stratification.

Example:
```python
from sklearn.model_selection import StratifiedKFold

skf = StratifiedKFold(n_splits=5, shuffle=True, random_state=42)
for train_idx, test_idx in skf.split(X, y):
    print("Train:", train_idx, "Test:", test_idx)
```
## 3. `StratifiedGroupKFold`

Description: Splits dataset into k folds by preserving class distribution (stratification) and ensuring that the same group is not represented in both training and validation sets.

Use case: Classification tasks with imbalanced labels and grouped data (e.g., multiple samples per patient, speaker, or device).

Key parameters:

n_splits: number of folds.

Requirement: Needs both labels (y) and groups.

Example:
```python
from sklearn.model_selection import StratifiedGroupKFold

sgkf = StratifiedGroupKFold(n_splits=5)
for train_idx, test_idx in sgkf.split(X, y, groups=groups):
    print("Train:", train_idx, "Test:", test_idx)
```

| Splitter               | Preserves Class Ratio | Handles Groups | Typical Use Case                      |
| ---------------------- | --------------------- | -------------- | ------------------------------------- |
| `KFold`                | ❌ No                  | ❌ No           | Regression or balanced classification |
| `StratifiedKFold`      | ✅ Yes                 | ❌ No           | Classification with class imbalance   |
| `StratifiedGroupKFold` | ✅ Yes                 | ✅ Yes          | Grouped classification with imbalance |
