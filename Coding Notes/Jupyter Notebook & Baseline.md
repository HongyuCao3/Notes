# Jupyter Notebook & Baseline

## Jupyter Notebook

- Use for **exploratory analysis** before writing scripts — not for final production code
- Key things to check during EDA:
  - Feature distributions, null rates, outliers
  - Whether your train/val split preserves the same distribution as the full dataset (affects method design)
  - Correlations between features and target
- Practical tips:
  - Use `%autoreload 2` at the top to auto-reload imported modules while editing
  - Use `display(df.head())` instead of `print` for better table rendering
  - Split into sections: Data Loading → EDA → Feature Engineering → Modeling
  - Keep cells short and focused — one idea per cell
  - Restart kernel and run all before submitting/sharing to catch hidden state bugs

## Baseline

- **Always find a baseline before designing your method** — baselines reveal what's hard and what's trivial
- [Kaggle](https://www.kaggle.com/) is the best source for dataset baselines and EDA notebooks:
  - Learn coding techniques from top notebooks
  - Baselines are almost always in Jupyter Notebooks
- What a good baseline tells you:
  - Which features matter most
  - What preprocessing actually helps
  - What performance level is "easy" vs requires clever methods
- Start simple: linear model or tree model often beats complex approaches on tabular data
