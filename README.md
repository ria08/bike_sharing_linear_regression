# Bike Sharing Demand Prediction (Linear Regression)

## Overview
This repository contains a linear regression analysis of daily bike-sharing demand for BoomBikes in the US. The goal is to identify the factors that most influence demand and build a model that can explain and predict daily bike rentals, helping the business prepare for post-pandemic recovery. The core analysis and model are implemented in the notebook `Assignment solution.ipynb`.

## Problem Statement
BoomBikes experienced significant revenue drops during the COVID-19 pandemic and needs a data-driven plan to recover. The company wants to understand:

1. **Which variables significantly predict bike demand.**
2. **How well those variables explain daily bike rentals.**

Using a dataset of daily bike rentals and related features (weather, seasonality, time), we build a model to quantify these effects and interpret the strongest drivers of demand.

## Dataset
The dataset used is `day.csv`, which contains daily bike rental data and associated features. Key fields include:

- **season**: 1 (spring), 2 (summer), 3 (fall), 4 (winter)
- **yr**: 0 (2018), 1 (2019)
- **mnth**: month (1–12)
- **holiday**: whether the day is a holiday
- **weekday**: day of the week
- **workingday**: whether the day is neither weekend nor holiday
- **weathersit**: weather category (clear/mild/moderate/extreme)
- **temp / atemp**: temperature measures
- **hum**: humidity
- **windspeed**: wind speed
- **cnt**: total rentals (target)

Full field definitions and licensing information are documented in `data dictionary.txt`.

## Approach
The notebook follows a standard linear regression workflow:

1. **Data Cleaning & Preparation**
   - Remove unused columns (`casual`, `registered`), since they sum to the target `cnt`.
   - Convert categorical fields into dummy variables.
   - Scale continuous variables using MinMaxScaler.
2. **Exploratory Data Analysis (EDA)**
   - Understand distributions, correlations, and seasonality.
   - Inspect target trends by year, season, and weather conditions.
3. **Modeling**
   - Split data into train/test (70/30).
   - Use RFE (Recursive Feature Elimination) with Linear Regression for feature selection.
   - Evaluate multicollinearity with VIF and refine features.
4. **Model Evaluation**
   - Fit the final OLS regression model with statsmodels.
   - Evaluate performance on training and test data using R² and adjusted R².

## Final Model (OLS)
The selected model explains a substantial portion of variance in daily rentals.

**Training Performance**
- **R²**: 0.833
- **Adjusted R²**: 0.830

**Test Performance**
- **R²**: 0.794
- **Adjusted R²**: 0.784

### Final Features
The final model includes the following predictors:

- `temp`
- `windspeed`
- `season_Spring`
- `season_Summer`
- `season_Winter`
- `yr_2019`
- `holiday_Not Holiday`
- `mnth_September`
- `weathersit_Extremely Moderate`
- `weathersit_Moderate`

## Key Conclusions
Based on the analysis and model results:

1. **Demand is higher in 2019 than 2018.**
2. **Demand increases from summer to fall and drops in winter.**
3. **Clear weather drives the highest rental counts; moderate/extreme weather reduces demand.**
4. **Outliers exist in humidity and windspeed, but they don’t strongly distort distributions.**
5. **The final model explains ~83% of variance in daily demand on training data.**

## Repository Structure
```
.
├── Assignment solution.ipynb   # Main analysis and modeling notebook
├── README.md                   # Project documentation (this file)
├── day.csv                     # Input dataset
├── data dictionary.txt         # Dataset description and license
└── Solution ppt.pdf            # Presentation of results
```

## How to Run
1. Ensure Python 3.x is installed.
2. Install required libraries:
   ```bash
   pip install numpy pandas matplotlib seaborn scikit-learn statsmodels
   ```
3. Open the notebook:
   ```bash
   jupyter notebook "Assignment solution.ipynb"
   ```
