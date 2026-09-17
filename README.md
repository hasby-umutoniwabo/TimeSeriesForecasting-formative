# Mobile Network Traffic Forecasting — Milan

Comparative study of sequential models (one-step-ahead forecasting) on the
Telecom Italia Big Data Challenge Milan dataset.

## Project structure
- `notebooks/` — step-by-step Colab notebooks (data pipeline, EDA, modeling)
- `src/` — reusable Python scripts
- `data/` — processed data outputs (not tracked in git, see notebooks to regenerate)
- `report/` — final report and supporting figures

## Setup
pip install -r requirements.txt

## Status
- [x] Data pipeline (memory-efficient loading + aggregation)
- [ ] Exploratory data analysis
- [ ] Model selection & related work
- [ ] Forecasting experiments
- [ ] Final report