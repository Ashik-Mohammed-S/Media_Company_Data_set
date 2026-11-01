# Next-Day Media View Forecasting

[![Validation](https://github.com/Ashik-Mohammed-S/Media_Company_Data_set/actions/workflows/validate.yml/badge.svg)](https://github.com/Ashik-Mohammed-S/Media_Company_Data_set/actions/workflows/validate.yml)

Forecast next-day show views using only observations available at the forecast origin.

Independent public portfolio work; historical educational notebooks remain under `historical/`. The current implementation and results described here take precedence over historical in-sample numbers.

## Data and approach

80 daily observations; 63 training targets and 16 final chronological test targets after lag construction.

Use lagged views, visitors, advertising and platform observations plus known calendar/trend features. Select Ridge regularization and compare the model with persistence using expanding-window training CV before final testing.

## Current full-data result

| Measure | Current analysis | Baseline where applicable |
| --- | --- | --- |
| MAE | 54,520 | 122,289 |
| RMSE | 73,379 | 173,367 |
| R² | 0.768 | -0.296 |

Results are specific to the documented dataset and split. See generated `results/analysis.json` after execution for full metrics and assumptions.

## Run locally

Use the Python version in `.python-version`, then:

```sh
python -m pip install -r requirements.txt
python scripts/fetch_data.py
python scripts/run_notebook.py --mode full
```

Reference data is committed under `dataset/`, directly or as reconstructable compressed parts. The downloader verifies checksums and restores stored data offline. See [DATA.md](DATA.md) and [dataset-sources.json](dataset-sources.json) for provenance and upstream terms. Package installation and the spaCy model, where needed, require network access on a fresh machine.

## Review the implementation

Inspect temporal ordering and the exclusion of unavailable current-day audience/ad totals. Start with [scripts/analysis.py](scripts/analysis.py), then the root notebook. The workflow validates dependencies, smoke checks and full-data notebook execution with dataset downloads disabled.

## Limitations

Only sixteen final test days are available. This is rolling one-step forecasting, not an unconditional multi-day forecast or evidence that advertising causes view growth.

[Method notes](ANALYSIS.md) · [All portfolio projects](https://github.com/Ashik-Mohammed-S/Ashik-Mohammed-S/blob/main/PORTFOLIO.md)
