# Mobile Network Traffic Forecasting — Milan

Comparative study of three sequential forecasting models (SARIMA, LSTM, and XGBoost) for one step ahead forecasting of mobile internet traffic, using the Telecom Italia Big Data Challenge dataset for Milan (November 2013 to January 2014, 10,000 grid areas, 10 minute intervals).

## Research question

How do different sequential models compare for one step ahead mobile network traffic forecasting, and how does their performance vary across geographical areas with different traffic characteristics?

## Project structure

```
notebooks/
  01_data_pipeline.ipynb   Memory efficient data loading and aggregation
  02_eda.ipynb             Exploratory analysis, ACF/PACF, seasonal decomposition
  03_modeling.ipynb        SARIMA, LSTM, and XGBoost: training, tuning, evaluation
results/
  plot_*.png               9 required forecast plots (3 models x 3 areas)
  table_*.csv              3 comparison tables (one per area)
  xgb_tuning_log.csv       XGBoost hyperparameter search results
  lstm_tuning_log.csv      LSTM hyperparameter search results
report/
  Mobile_Traffic_Forecasting_Report.docx   Full written report
README.md
requirements.txt
.gitignore
```

## Setup

```bash
pip install -r requirements.txt
```

A free Kaggle account is needed to reproduce the data pipeline in `notebooks/01_data_pipeline.ipynb`, since it downloads the dataset from Kaggle. Google Colab is recommended for running the notebooks, since the full pipeline needs meaningful RAM and disk space to process the raw ~20.8 GB dataset. Full step by step download and setup instructions are included at the top of that notebook.

## Dataset

Source: "sms-call-internet-mi" dataset, originally released by Telecom Italia as part of the Big Data Challenge, and hosted on Harvard Dataverse. Because Dataverse requires a manual "guestbook" form submission before releasing files, which cannot be automated, this project uses a complete mirror of the same dataset published on Kaggle as `freckled/telecom`.

Citation for the original dataset:

Barlacchi, G., De Nadai, M., Larcher, R. et al. "A multi-source dataset of urban life in the city of Milan and the Province of Trentino." Scientific Data 2, 150055 (2015). https://doi.org/10.1038/sdata.2015.55

## How to reproduce

1. Run `notebooks/01_data_pipeline.ipynb` end to end. This downloads the raw dataset, aggregates it into a single compact array, and saves it as `traffic_matrix.npz`.
2. Run `notebooks/02_eda.ipynb` to reproduce the exploratory analysis and figures.
3. Run `notebooks/03_modeling.ipynb` to train and evaluate all three models, and regenerate everything in `results/`.

## Models compared

- **SARIMA**: classical statistical baseline, with the daily seasonal cycle removed manually before fitting a simple ARIMA model on the remainder.
- **LSTM**: recurrent neural network trained on sliding windows of scaled traffic values, tuned via grid search over hidden units and training epochs.
- **XGBoost**: gradient boosted trees trained on lag features, tuned via grid search over tree depth and number of trees.

## Key results

Across the three highest traffic areas tested (GridID 5161, 5059, and 5259), XGBoost achieved the lowest MAE and MAPE in every area, while SARIMA trained in under one second per area and stayed close behind in accuracy. LSTM, even after tuning, was the most expensive model to train and did not clearly outperform the simpler alternatives. Full numbers are in `results/table_5161.csv`, `table_5059.csv`, and `table_5259.csv`, and full discussion is in the report.

## Report

The complete written report, covering related work, memory management, exploratory analysis, methodology, results, failure analysis, and conclusions, is in [this report](https://docs.google.com/document/d/1Wxr0b_060VlhjQM1rGFaZVGxwzlRteTDiFfayU4TvPs/edit?usp=sharing).

## Video presentation

[Watch the video presentation](https://www.youtube.com/watch?v=-dxEa5lG1-k)

## Author

Hasbiyallah Umutoniwabo
