# Palm Oil Production Forecasting & Early Warning System

Forecasting TBS Production Using Historical Production, Agronomic, Weather, and Operational Data

## Project Overview

Production forecasting is an important part of operational planning in the palm oil industry. Production outcomes can be influenced by historical production patterns, plantation characteristics, weather conditions, fertilization, and operational disruptions.

This project develops an end-to-end analytical workflow to forecast monthly Fresh Fruit Bunch (TBS) production at the estate level and identify potential production deviations through an early warning system.

The project covers the complete workflow from data preparation and validation to exploratory analysis, feature engineering, forecasting model evaluation, and dashboard development.

> **Note:** This project uses simulated data for portfolio and analytical demonstration purposes. The dataset does not represent actual company or plantation data.

## Business Problem

Production data from multiple estates can contain different patterns related to seasonality, plantation age, weather conditions, fertilization, and operational activities.

The objective of this project is to develop a forecasting workflow that can:

- Forecast monthly TBS production at estate level
- Incorporate historical production, weather, agronomic, and operational factors
- Compare different forecasting approaches
- Evaluate forecasting performance using MAE, RMSE, and MAPE
- Identify potential production deviations through an early warning mechanism
- Present forecasting results through an interactive dashboard

## Project Objectives

1. Prepare and validate estate-level production and supporting data.
2. Explore production trends, seasonality, and relationships between production and operational or environmental variables.
3. Engineer features for production forecasting.
4. Develop and compare multiple forecasting models.
5. Evaluate model performance on an out-of-sample test period.
6. Develop an early warning mechanism based on forecast deviations.
7. Present the results through a Power BI dashboard.

## Dataset

The project uses simulated monthly data covering:

- **Period:** January 2019 – December 2025
- **Estates:** 10
- **Regions:** Sumatra, Kalimantan, Sulawesi
- **Frequency:** Monthly
- **Expected estate-month observations:** 840

### Data Domains

| Dataset | Description |
|---|---|
| Estate Master | Estate identity, region, area, and planting year |
| Weather Data | Monthly rainfall and rainy days |
| Operation Data | Fertilizer application, working days, and operational disruption |
| Production Data | TBS, CPO, and kernel production |

The main relationship is based on `estate_id` + `date`.

## Project Workflow

```text
Raw Data
   ↓
Data Cleaning & Validation
   ↓
Exploratory Data Analysis
   ↓
Feature Engineering
   ↓
Forecasting Models
   ↓
Model Evaluation
   ↓
Early Warning System
   ↓
Power BI Dashboard
```

## Data Preparation

The raw data was intentionally designed to contain operational-style data quality issues, including missing values, duplicate estate-month records, invalid values, and production outliers.

Validation covered:

- data types and structure
- duplicate estate-month keys
- estate ID consistency
- date range consistency
- missing values
- numerical range checks
- production business rules
- extraction-rate checks
- cross-table estate-date consistency

After cleaning, the transactional datasets contain 840 estate-month observations each with no remaining missing values or duplicate estate-month keys in the cleaned outputs.

## Exploratory Data Analysis

EDA focused on:

- annual production trends
- monthly seasonality
- regional and estate-level production/yield
- plant age and productivity
- rainfall and productivity
- fertilizer intensity and productivity
- operational disruption and productivity
- correlation analysis
- production and extraction-rate distributions

Key observations from the simulated data include a recurring monthly production pattern, differences in productivity between estates/regions, and non-identical relationships between production and environmental or operational variables.

## Feature Engineering

Features were created across five groups:

### Time

- `month`
- `quarter`
- `month_sin`
- `month_cos`

### Agronomy

- `area_ha`
- `plant_age_years`
- `fertilizer_kg_per_ha`

### Weather

- `rainfall_mm`
- `rainy_days`
- `rainfall_lag_1`
- `rainfall_lag_3`
- `rainfall_3m_avg`
- `rainfall_6m_avg`

### Operations

- `working_days`
- `disruption_days`

### Historical Production

- `tbs_lag_1`
- `tbs_lag_3`
- `tbs_lag_6`
- `tbs_lag_12`
- `tbs_rolling_mean_3`
- `tbs_rolling_mean_6`
- `tbs_rolling_mean_12`
- `tbs_growth_1m`
- `tbs_growth_12m`

The target for the main forecasting task is `tbs_production_ton`.

## Forecasting Methodology

The data is split chronologically:

- **Training:** 2019–2024
- **Testing:** 2025

The following models are compared:

1. Naive Forecast
2. Seasonal Naive
3. Holt-Winters / Exponential Smoothing
4. SARIMA
5. Random Forest Regressor

Evaluation metrics:

- MAE
- RMSE
- MAPE

## Model Evaluation

On the 2025 test set, the evaluated models produced the following results:

| Model | MAE | RMSE | MAPE |
|---|---:|---:|---:|
| Naive | 975.95 | 1,228.36 | 9.90% |
| Seasonal Naive | 824.11 | 1,036.15 | 8.65% |
| Holt-Winters | 788.14 | 1,001.91 | 8.43% |
| SARIMA | 13,765.84 | 41,841.31 | 147.54% |
| Random Forest | **160.65** | **255.66** | **1.65%** |

Within this simulated dataset and evaluation period, Random Forest produced the lowest MAE, RMSE, and MAPE among the tested models.

## Forecast Output

The Random Forest forecast output contains 120 estate-month observations for 2025 (10 estates × 12 months).

Aggregate 2025 values from the project:

- Actual TBS: approximately **1.170 million tons**
- Forecast TBS: approximately **1.173 million tons**

These results represent an out-of-sample backtesting exercise on simulated data, not a live production forecasting system.

## Early Warning System

The next stage uses actual-vs-forecast deviation to classify potential production deviations into:

- Normal
- Warning
- Critical

The alert thresholds are predefined analytical thresholds for this portfolio project and should not be interpreted as industry standards.

## Dashboard

A Power BI dashboard is planned to present:

- actual vs forecast TBS
- regional and estate production
- model performance
- forecast deviation
- alert status

## Tools & Technologies

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Statsmodels
- Jupyter Notebook
- Power BI (dashboard stage)

## Limitations

- The dataset is synthetic and does not represent actual plantation operations.
- Forecasting performance is evaluated on a single 2025 holdout period.
- The alert thresholds are analytical assumptions for portfolio demonstration.
- A production-ready system would require ongoing model calibration using new actuals and field conditions.
- Future forecasting beyond the historical test period would require a controlled recursive forecasting process for lagged production features.

## Future Improvements

- Add actual operational/field data when available.
- Implement rolling-origin or walk-forward validation.
- Compare additional forecasting algorithms and hyperparameter tuning strategies.
- Add automated model retraining and monitoring.
- Extend forecasting to CPO and kernel production.
- Complete the Power BI early warning dashboard.

## Author

**Adinda Hermawan**  
Mathematics Graduate | Data Analytics & Forecasting Portfolio
