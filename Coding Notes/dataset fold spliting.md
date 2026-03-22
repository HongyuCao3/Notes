# Cross-Validation Splitters (scikit-learn)

## Quick Decision

| Splitter | Use When |
|----------|----------|
| `KFold` | Regression or balanced classification, no groups |
| `StratifiedKFold` | Classification with class imbalance |
| `StratifiedGroupKFold` | Imbalanced classes + grouped data (e.g., multiple samples per patient) |

---

## KFold — General Purpose

```python
from sklearn.model_selection import KFold

kf = KFold(n_splits=5, shuffle=True, random_state=42)
for train_idx, val_idx in kf.split(X):
    ...
```

- Use `shuffle=True` to avoid data ordering bias

---

## StratifiedKFold — Preserves Class Distribution

```python
from sklearn.model_selection import StratifiedKFold

skf = StratifiedKFold(n_splits=5, shuffle=True, random_state=42)
for train_idx, val_idx in skf.split(X, y):  # needs y
    ...
```

- Each fold has the same class ratio as the full dataset
- Always use for classification when classes are imbalanced

---

## StratifiedGroupKFold — Groups Must Not Leak

```python
from sklearn.model_selection import StratifiedGroupKFold

sgkf = StratifiedGroupKFold(n_splits=5)
for train_idx, val_idx in sgkf.split(X, y, groups=groups):  # needs both y and groups
    ...
```

- Ensures the **same entity** (patient, user, device) never appears in both train and val
- Critical for avoiding data leakage in grouped datasets

---

## Tip: Why Stratification Matters

Without stratification on imbalanced data, some folds may have very few positive samples — metrics become unreliable and training is inconsistent.
