# Recession Prediction with Machine Learning

**Fixed Income Theory · MBA coursework, The University of Scranton**

[!\[Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Greg-Duggan/Fixed-Income-Theory/blob/main/GDuggan_Fixed_Income.ipynb)

This project tests how well the yield curve, alone and combined with labor and inflation data, can predict U.S. recessions as defined by the NBER. It compares a logistic regression baseline with a random forest and validates both out-of-sample against the 2001, 2008–09, and 2020 recessions.

## Research question

How does the 10-year minus 2-year Treasury spread relate to NBER recessions, and how much does adding unemployment and inflation improve recession forecasts six months ahead?

## Data

All data is pulled live from the Federal Reserve Bank of St. Louis (FRED) API.

|Series|FRED code|Use|
|-|-|-|
|10-year minus 2-year Treasury spread|`T10Y2Y`|Yield curve signal (averaged to monthly)|
|NBER recession indicator|`USREC`|Target (1 = recession)|
|Unemployment rate|`UNRATE`|Labor market signal|
|Consumer Price Index|`CPIAUCSL`|Converted to year-over-year inflation|

## Methodology

1. **Exploratory analysis.** Visualized yield-curve inversions and the 2022–24 "un-inversion," and measured the spread's correlation with recessions. The relationship is strongly non-linear, so a simple correlation understates it.
2. **Models.** Logistic regression as a baseline, and a random forest to capture non-linear relationships. Both use balanced class weights, because recessions are rare.
3. **Six-month lead.** The target is whether the economy is in recession six months later.
4. **Out-of-sample validation (Section 6).** For each test recession, models are trained only on data from before the test window.
5. **Explainability.** SHAP values and random forest feature importance show which indicators drive the predictions.

## Results

### Out-of-sample backtests

Each model is trained only on data before the test window and predicts recessions six months ahead.



|Test window|Model|Recall|Precision|ROC AUC|
|-|-|-|-|-|
|Dot-com (2001)|Logistic Regression|0.00|0.00|0.71|
|Dot-com (2001)|Random Forest|0.00|0.00|0.36|
|GFC (2008–09)|Logistic Regression|0.00|0.00|0.75|
|GFC (2008–09)|Random Forest|0.00|0.00|0.74|
|COVID (2020)|Logistic Regression|0.00|0.00|0.66|
|COVID (2020)|Random Forest|0.00|0.00|0.29|

*Recall* is the share of recession months the model flagged; *precision* is the share of flagged months that were recessions; *ROC AUC* measures how well the predicted probabilities rank recession months above normal ones (0.5 = chance).

### Earlier in-sample analysis

Sections 3–5 of the notebook train on data through 2023 and then backtest the Great Financial Crisis. Because the crisis is inside the training data, the perfect scores there reflect memorization rather than forecasting. They are kept to show how the analysis developed, and Section 6 is the reliable test.

## Limitations

* **Few recessions.** There have been only a handful of U.S. recessions since 1976, so every test window has few positive months and results can swing on one or two predictions.
* **Every recession is different.** The 2020 recession was caused by a pandemic shock that no economic indicator could foresee.
* **NBER dating lags.** Recessions are officially dated months after the fact, so a real-time forecaster would not know the target as soon as this backtest does.
* **The 2024–25 test window contains no recessions.** High accuracy there only means the model correctly predicted "no recession."

## Future work

* Test 3-, 9-, and 12-month lead times.
* Try gradient boosting (XGBoost) and add indicators such as credit spreads.
* Build a live dashboard that updates from FRED monthly.

## Setup

```bash
git clone https://github.com/Greg-Duggan/Fixed-Income-Theory.git
cd Fixed-Income-Theory
pip install -r requirements.txt
export FRED\_API\_KEY=your\_key\_here   # free key: https://fred.stlouisfed.org/docs/api/api\_key.html
jupyter notebook GDuggan\_Fixed\_Income.ipynb
```

Or open the notebook in Google Colab with the badge above; it will ask for your FRED API key when it runs.

**What the results show:** Logistic regression ranks recession months above normal months well out of sample (ROC AUC 0.66–0.75), but its probabilities stayed below the default 50% cutoff, so it never issued a recession call. The random forest, which scored perfectly in-sample, falls to or below chance on two of three recessions, a clear sign of overfitting. The simpler model generalizes better.

