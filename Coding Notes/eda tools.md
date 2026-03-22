# EDA Tools

## missingno — Visualize Missing Data

- `pip install missingno`
- Quickly reveals **where** and **how** data is missing

```python
import missingno as msno
import pandas as pd

msno.matrix(df)      # row-level view — brightness = completeness
msno.bar(df)         # per-column missing count and ratio
msno.heatmap(df)     # correlation of missingness between columns
msno.dendrogram(df)  # cluster columns by similar missing patterns
```

- **heatmap** is most useful: if two features always go missing together, they likely share a source
- **matrix** is best for spotting block-shaped missing patterns (e.g., missing from row 500 onward)

---

## ydata-profiling — Automated EDA Report

- `pip install ydata-profiling` (formerly pandas-profiling)
- Generates a full HTML report from a DataFrame

```python
from ydata_profiling import ProfileReport

profile = ProfileReport(df, title="EDA Report")
profile.to_file("report.html")        # save to file
profile.to_notebook_iframe()          # display in notebook
```

- Covers: distributions, correlations, missing values, duplicates, outliers
- Best for **first look** at a new dataset — saves time vs manual inspection

---

## pandas built-ins (quick checks)

```python
df.info()              # dtypes, null counts, memory
df.describe()          # stats for numeric columns
df.isnull().sum()      # null count per column
df.duplicated().sum()  # number of duplicate rows
df.value_counts()      # frequency of each value (Series)
df.corr()              # correlation matrix
```
