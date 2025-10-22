# Buy Now, Pay Later Project Group 44

Maintained by group members:

Lachy Bowker

Dion Papadopoulos

Parth Agarwal

Andy Chen

Josh Jones

## Project Overview

This project aims to create a ranking of potential merchants to onboard to a BNPL firm, utilising metrics potential growth and loss, current takings and potential future revenue. The final ranking is a composite of these metrics, and are split into seperate business areas to see where the firm can profit the most.

Provided BNPL transaction data is synthetically generated individual transaction data, user data and merchant data.
Additionally, income data for SA2 is sourced from the ABS, as is the SA2 to postcode dataset.

Note: Make sure to read the `README.md` located in `./data/README.md` for extra details on the synthetically generated data.

## Repository Structure

- `notebooks/`
  - `00_approach_summary.ipynb` — Project overview, approach, issues, assumptions, limitations
  - `01_etl.ipynb` — Data curation, joins, outlier handling, segmentation
  - `02_income_outlier.ipynb` — SA2 income analysis and binning
  - `03_fraud_model.ipynb` — Tiered fraud probability (direct, user-decay, model), EB aggregation, diagnostics
  - `04_time_series.ipynb` — Time-series exploration of transactions, composite rankings of growth
  - `05_final_rankings.ipynb` — Composite rankings (takings, loss potential, growth)
  - `06_plots.ipynb` — Exploratory plots and summaries
- `data/`
  - `tables/` — provided source tables (parquet/csv)
  - `curated/` — pipeline outputs (merchant_transactions, agg_by_userbiz, rankings)
  - `final_ranks/` — final composite and per-segment rankings
- `artifacts/` — model/pipeline outputs written by notebooks (e.g., `fraud_outputs/`)
- `plots/` — saved figures (calibration, lift, errors, segment EFLR)

## How to Run

1. Environment

   - Python 3.9+
   - Install dependencies: `pip install -r requirements.txt`
   - Local PySpark is used; the notebooks set reasonable defaults for memory/shuffle
   - Spark environments may differ between notebooks based on operating system of editor

2. Recommended order (open and run notebooks in this sequence):

   - `00_approach_summary.ipynb` (read-only)
   - `01_etl.ipynb`
   - `02_income_outlier.ipynb`
   - `03_fraud_model.ipynb`
   - `04_time_series.ipynb`
   - `05_final_rankings.ipynb`
   - `06_plots.ipynb`

3. Data expectations
   - Source tables under `data/tables/` must be present
   - Notebooks write curated outputs to `data/curated/` and rankings to `data/final_ranks/`

## Reproducibility Notes

- Paths in notebooks are relative to the `notebooks/` directory (e.g., `../data/...`)
- Outputs are overwritten to keep a clean state (idempotent runs)
- Some steps (window operations) warn about single-partition execution on local; for larger scale, configure Spark partitions and executors accordingly
- All random processes use fixed seeds `np.random.seed(42)` to ensure reproducibility
