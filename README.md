# DSA-210-Project

## Project Overview

This project analyzes how game updates and major Steam discount events influence concurrent player counts—both immediately and in the longer term—using data from SteamCharts and the Steam Store API. By quantifying these effects, we aim to help developers optimize content-release timing and discount strategies to maximize engagement and retention.

## Objectives

1. **Short- vs. Long-Term Impact**

   - Measure immediate (month-over-month) and sustained (multi-month) changes in player counts after updates and discounts.

2. **Discount Effectiveness**

   - Compare average player counts before, during, and after sale months.
   - Quantify retention: do numbers drop back after the sale ends?

3. **Update Impact**

   - Assess the boost from major content drops (DLCs, expansions, big patches).
   - Differentiate between major and minor updates.

4. **Category & Genre Comparison**

   - Identify which game categories (e.g. Indie vs. AAA) see the largest relative gains.
   - Explore genre-tag influences.

5. **Seasonality & External Factors**

   - Detect recurring seasonal peaks (holidays, summer).
   - Examine whether sale timing interacts with seasonality.

## Motivation

- **Industry Insights:** Understand how discounts and updates drive player re-engagement.
- **Revenue Strategy:** Inform pricing models by measuring relative “price elasticity.”
- **Data-Driven Decisions:** Use historical trends to predict the success of future content drops and sales.

## Dataset

- **app\_id**: Steam AppID
- **game\_name**: Title
- **category**: One of {AAA, Indie, 4X, Story-Based, FPS}
- **genres**: Semicolon-separated Steam genre tags
- **month**: Year-month (`YYYY-MM`)
- **avg\_players**: Monthly average concurrent players (SteamCharts)
- **price**: Current list price (USD)
- **sale\_flag**: 1 if flagged as “sale” month, else 0
- **had\_update**: 1 if a major update/DLC/patch occurred, else 0

## Data Sources

- **SteamCharts** (`https://steamcharts.com/app/{app_id}`) → `avg_players`
- **Steam Store API** (`/api/appdetails`) → `price_overview`, `genres`
- **Steam News API** (`ISteamNews/GetNewsForApp/v2`) → update flags
- **Manual Mapping** → category and sale-month definitions

## Exploratory Data Analysis (EDA)

1. **Time-Series Decomposition & Rolling Averages**
   - Revealed clear seasonal cycles (annual peaks around holidays) and longer-term upward trends in many titles.
2. **Distribution by Category**
   - Boxplots with 10 k-unit ticks and borders highlighted that Indie games often have lower absolute player counts but wider relative variation.
3. **Correlation Analysis**
   - Price & sale\_flag showed virtually no linear correlation with avg\_players (r≈0).
   - `had_update` exhibited a small positive correlation (r≈+0.09).
4. **Total Player Counts**
   - Summed across all 50 games, the aggregate series peaks sharply during major sale months.

## Hypotheses & Findings

### Hypothesis 1: Sale vs Non-Sale Player Counts

- **Test:** Welch’s one-tailed t-test
- **Result:** t = 3.21, p = 0.0007 → **Reject H₀**
- **Conclusion:** Sale months have a statistically significant higher mean player count.

### Hypothesis 2: Indie vs AAA Median Percent Gain

- **Test:** One-tailed Mann–Whitney U test
- **Result:** U = 1 254 300, p = 0.018 → **Reject H₀**
- **Conclusion:** Indie titles see a larger median percent bump during sales than AAA titles.

### Hypothesis 3: Price Elasticity

- **Test:** Pearson’s correlation between `price` and percent gain
- **Result:** r = –0.05, p = 0.34 → **Fail to reject H₀**
- **Conclusion:** No significant linear relationship between list price and relative sale lift.

### Hypothesis 4: Update-Driven Spikes

- **Test:** One-tailed one-sample t-test on update-month pct\_changes
- **Result:** t = 5.48, p = 0.00001 → **Reject H₀**
- **Conclusion:** Major updates reliably produce a positive spike in player counts.

## Limitations & Future Work

- **Sale Flag Simplification:** We used fixed calendar months for “sale.” Scraping actual discount percentages could refine this.
- **Lag Effects:** We tested only immediate month-to-month differences; multi-month “carry-over” effects deserve study.
- **Genre Decomposition:** Future analysis could explode multi-genre tags and model mixed-effect contributions.
- **Time-Series Modeling:** ARIMA or causal impact models could quantify the duration of sale/update effects.
  
## Machine Learning Pipeline

- **Objective:** Forecast next‐month changes in concurrent player counts for each game.  
- **Modeling Approach:**  
  - Compared **Random Forest**, **Decision Tree**, and **kNN** regressors.  
  - Used **time‐series cross‐validation** for hyperparameter tuning.  
- **Final Model:** Random Forest Regressor  
  - **Performance (hold‐out):**  
    - R² ≈ 0.30  
    - MAE ≈ 3 037 players  
    - RMSE ≈ 6 790 players  
- **Deployment:**  
  - Serialized model → rf_player_change.pkl
  - Serialized scaler → scaler_player_change.pkl  
  - Batch script → predict_change.py producing predictions.csv each month  

---
I acknowlage using LLM for grammer and manual data gathering
