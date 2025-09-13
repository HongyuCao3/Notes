# EDA Tools

## missingno
`missingno` is a Python library for **visualizing missing data** in datasets.  
It helps detect **patterns, distribution, and correlations** of missing values during EDA.

### Main Functions

 - Matrix Plot
    ```python
    msno.matrix(df)
    ```

    Shows missing values across rows and columns.

    Brightness/opacity indicates data completeness.

 - Bar Plot
    ```python
    msno.bar(df)
    ```

    Displays non-missing count and missing ratio for each column.

    Good for comparing feature completeness.

 - Heatmap
    ```python
    msno.heatmap(df)
    ```

    Correlation map of missing values between features.

    Helps find variables that tend to be missing together.

 - Dendrogram
    ```python
    msno.dendrogram(df)
    ```

      Hierarchical clustering of missing-value correlations.

      Useful for identifying variable groups with similar missing patterns.

###  Example Usage
```python
import missingno as msno
import pandas as pd

# Sample data
df = pd.DataFrame({
    "A": [1, 2, None, 4, 5],
    "B": [1, None, None, 4, 5],
    "C": [None, 2, 3, None, 5],
})

# Visualizations
msno.matrix(df)
msno.bar(df)
msno.heatmap(df)
msno.dendrogram(df)
```
---
