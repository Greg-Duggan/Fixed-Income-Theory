📉 AI-Driven Recession Prediction

Fixed Income Theory: Macroeconomic Indicators & Machine Learning

🚀 Project Overview

This project leverages Machine Learning to predict NBER-defined recessions in the U.S. We specifically analyze the predictive power of:T10Y2Y: The 10-Year vs. 2-Year Treasury spread (The Yield Curve).

UNRATE: The Unemployment Rate.

CPIAUCSL: Consumer Price Index (Inflation).

By addressing class imbalance (since recessions are rare) and non-linear relationships, this study develops a robust Random Forest Classifier to provide early warning signals for financial markets.

❓ The Research Question"How does the T10Y2Y spread relate to NBER recession indicators, and to what extent can it—combined with other macro variables—predict future economic downturns?"

🛠 Methodology

📡 Data Acquisition: Real-time data fetched via the FRED API.

📊 Exploratory Data Analysis (EDA): Visualizing yield curve inversions. 

Finding: Strong non-linear patterns despite weak linear correlation.

🤖 Model Development:

Logistic Regression: Established a baseline.

Random Forest: Trained to handle complex, non-linear economic signals.

Class Balancing: Used class_weight='balanced' to ensure the model doesn't ignore recession events.

🧪 Evaluation: Rigorous backtesting against the Great Financial Crisis (GFC).

🔮 XAI (Explainability): Using Feature Importance to see what "drives" the AI’s decision.

Insights:

🌲 Random Forest Wins: Non-linear models significantly outperformed traditional regression.

⚖️ The "Secret Sauce": Adding CPI and Unemployment created a "perfect" prediction profile for the GFC.

💡 Feature Importance: Inflation (CPI) was the top driver (40.6%), followed by the Spread (30.6%) and Unemployment (28.8%).

🏁 Conclusion

While the yield curve is a vital "pulse," its predictive power is supercharged when integrated with inflation and labor data. Our model successfully predicted the GFC 6 months in advance, proving that AI can offer invaluable foresight for strategic decision-making in fixed income.

🔮 Future Work

⏱️ Variable Lead Times: Testing 3, 9, and 12-month forecasts.

🧠 Advanced Models: Experimenting with XGBoost and LSTMs.

🖥️ Live Dashboard: Creating a real-time monitor using updated FRED data.

💻 Setup & UsageClone: git clone [your_repo_url]Install: pip install -r requirements.txtKey: Insert your FRED API Key into the notebook.Run: Execute [your_notebook_name].ipynb to reproduce these findings!
