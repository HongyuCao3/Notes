# Metrics & Result Saving

## What to Record Per Run

- `dataset_name`, `model_name`, `args/hyperparameters`, `metric values`, `timestamp`
- Consistent keys make it easy to compare runs across experiments

## Two Saving Strategies

### Directory-based (for logs, per-run outputs)
- Path pattern: `./outputs/{dataset}/{model}/{args}.json`
- Each run writes a new file — use auto-increment to avoid overwrites:
  ```python
  def get_next_filename(base_path: Path, extension="csv") -> Path:
      index = 0
      while True:
          path = base_path.with_name(f"{base_path.stem}_{index}.{extension}")
          if not path.exists():
              return path
          index += 1
  ```

### DataFrame-based (for metrics summary)
- One CSV/parquet file, one row per run
- Columns: `dataset`, `model`, `metric1`, `metric2`, `timestamp`, `args...`
- Easy to load and compare with `pd.read_csv()` + filter/groupby
- Append new rows with `pd.concat` or `df.to_csv(mode='a', header=False)`

## Practical Tips

- Save both **raw outputs** (predictions, embeddings) and **aggregated metrics** — raw lets you recompute metrics later
- Always save the config/args alongside results for reproducibility
- Use `json.dumps(vars(args))` to serialize argparse namespace
- For ML experiments, consider [MLflow](https://mlflow.org/) or [Weights & Biases](https://wandb.ai/) for automatic tracking
