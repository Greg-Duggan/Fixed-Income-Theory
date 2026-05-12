# Fixed-Income-Theory
For my Fixed Income Theory Class
AI-Driven Recession Prediction using Macroeconomic Indicators

Project Overview

This project explores the use of machine learning models to predict NBER-defined recessions in the United States, with a particular focus on the 10-Year Treasury Constant Maturity Minus 2-Year spread (T10Y2Y), Unemployment Rate (UNRATE), and Consumer Price Index (CPIAUCSL). Recognizing the complexities of economic forecasting, including class imbalance (recessions are rare events) and non-linear relationships, this study develops and evaluates various classification models, culminating in a robust Random Forest Classifier.

The goal is to demonstrate the potential of AI to enhance foresight in the fixed income space by providing early and accurate warnings of economic downturns.

Research Question
The core research question addressed is:

"How does the 10-Year Treasury Constant Maturity Minus 2-Year spread (T10Y2Y) relate to NBER recession indicators, and to what extent can this spread, in conjunction with other macroeconomic variables, be used to predict future recessions?"

Methodology
Data Acquisition: Time series data for T10Y2Y (Spread), USREC (NBER Recession Indicator), UNRATE (Unemployment Rate), and CPIAUCSL (Consumer Price Index) were fetched from the FRED database.
Exploratory Data Analysis (EDA): Initial analysis involved visualizing the yield curve's behavior, particularly during inversion cycles, and quantifying its correlation with recession indicators. This revealed a weak linear relationship but strong non-linear patterns.
Model Development:
Logistic Regression: Baseline models were developed using the Spread alone, and then extended with UNRATE and CPI. Class imbalance was addressed using class_weight='balanced'.
Random Forest Classifier: Non-linear models were trained, first with Spread only, and then with the extended feature set, also incorporating class_weight='balanced'.
Backtesting & Evaluation: Models were rigorously backtested on historical recessions, notably the Great Financial Crisis (GFC, Dec 2007 - Jun 2009), to assess their recall, precision, and F1-score for recession prediction.
Lead Time Prediction: A lagged target variable (Recession_6_Months_Ahead) was created to evaluate the best model's ability to predict recessions 6 months in advance.
Explainability (XAI): Feature importance analysis was conducted to understand the drivers behind the most effective models.
Key Findings
Model	Features Used	GFC Recall (Class 1)	GFC F1-Score (Class 1)
Initial Logistic Regression	Spread only	0.00	0.00
Extended Logistic Regression (with class_weight='balanced')	Spread, Unemployment_Rate, CPI	0.30	0.46
Random Forest Classifier (Spread only)	Spread only	0.60	0.75
Random Forest Classifier (Extended Features with class_weight='balanced')	Spread, Unemployment_Rate, CPI	1.00	1.00
Lagged Random Forest Classifier (6-month lead)	Spread, Unemployment_Rate, CPI	1.00	1.00
Superiority of Random Forest: Non-linear models like Random Forest significantly outperformed Logistic Regression, even with fewer features, demonstrating the complex nature of recession signals.
Importance of Extended Features: The inclusion of Unemployment_Rate and CPI dramatically improved model performance, leading to perfect recall and F1-scores during the GFC when combined with a Random Forest Classifier and balanced class weights.
Feature Contributions: Feature importance analysis revealed that CPI (inflationary pressures) was the most influential factor (0.406), followed by the Spread (0.306) and Unemployment Rate (0.288) in the best-performing model.
Lead Time Prediction: The Random Forest model, when trained on a 6-month lagged target, successfully predicted the GFC recession with perfect recall 6 months in advance, showcasing its potential for proactive economic risk management.
Conclusion
Predicting economic recessions is a challenging but critical task. This project demonstrates that while the yield curve spread remains a vital indicator, its predictive power is significantly enhanced when integrated with other key macroeconomic health indicators (like CPI and Unemployment Rate) within a sophisticated, non-linear machine learning framework such as a Random Forest Classifier. The ability to predict recessions with a lead time offers invaluable insights for strategic decision-making in financial markets and economic policy.

Other Potential Uses and Future Work
Other Lead Times: Investigate the model's performance for predicting recessions at different lead times (e.g., 3, 9, 12 months).
Alternative Models: Explore more advanced time-series models (e.g., XGBoost, Support Vector Machines, LSTMs) for further performance gains.
Optimal Thresholding: Implement techniques for dynamic optimal thresholding rather than relying solely on default classification thresholds.
Sensitivity Analysis: Conduct sensitivity analyses to understand model robustness under various economic scenarios.
Quantifying Uncertainty: Incorporate methods to quantify the uncertainty of predictions, providing a more complete picture of economic risk.
Real-time Monitoring Dashboard: Develop a dashboard for real-time monitoring of recession probabilities using updated FRED data.
Setup and Usage
To replicate this analysis:

Clone the Repository:
git clone [your_repo_url]
cd [your_repo_name]
Install Dependencies:
pip install -r requirements.txt # (or manually install fredapi, shap, pandas, matplotlib, sklearn, seaborn)
FRED API Key: Obtain a free API key from FRED (Federal Reserve Economic Data) and replace 'YOUR_API_KEY' in the notebook, or set it as an environment variable.
Run the Notebook: Open and execute the Jupyter/Colab notebook ([your_notebook_name].ipynb) to run the analysis and reproduce the findings.
