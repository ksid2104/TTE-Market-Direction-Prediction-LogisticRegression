# TTE-Market-Direction-Prediction-LogisticRegression

In this project, I explore the use of logistic regression to predict short-term market direction based on historical data from TotalEnergies (TTE). It combines **technical analysis**, **financial indicators**, and **machine learning modeling**, with a focus on explainability and a preliminary trading strategy.

---

## 📌 Objectives

- Use historical data from TTE starting in 2000  
- Add classic technical indicators (MA, RSI, Sharpe Ratio, etc.)  
- Build a target variable (upward or downward price movement)  
- Train a logistic regression model with time-based validation  
- Compare performance using raw vs. engineered features  
- Simulate a trading strategy filtered by confidence score (> 75%)  

---

## 📊 Methodology

- Libraries: `pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn`, `yfinance`  
- Model: `LogisticRegression` from scikit-learn  
- Temporal split: `TimeSeriesSplit` (preserves causality)  
- Visualization: ROC curve, confusion matrix, model coefficients  

---

## 🧪 Results

### 🎯 Model performance

- **Using raw features**:
  - ROC AUC: **0.76**
  - Precision*: **0.705**
  - Recall*: **0.70**

- **Using selected features**:
  - ROC AUC: **0.80**
  - Precision*: **0.72**
  - Recall*: **0.72**

> * Simple average between precision and recall across both classes (`0 = down`, `1 = up`)

---

### 📉 Backtest results (confidence > 75%)

| Metric                             | Value        |
|-----------------------------------|--------------|
| **Overall cumulative return**     | **-17.51%**  |
| Initial capital (base 1.0)        | 1.0000       |
| Final capital                     | 0.8249       |
| Number of trades executed         | 316          |
| Max daily return                  | +3.62%       |
| Min daily return                  | -3.16%       |
| Peak capital value                | 1.1114       |
| Max performance                   | +11.14%      |
| Lowest capital value              | 0.8175       |
| Min performance                   | -18.25%      |

---

### ⏱️ Strategy performance over time

- **📈 Growth phase (25/04/2021 → 24/04/2024)**  
  → Capital increased from **1.0000** to **1.1114** → **+11.14%**

- **📉 Decline phase (24/04/2024 → 15/07/2025)**  
  → Capital dropped to **0.8249** → **-17.14%** from the peak

These results show that the model has reasonable predictive power, but the trading strategy is **highly volatile** and struggles with **loss management**.

---

## 🔧 Areas for Improvement

- Add a **stop-loss mechanism** to limit drawdowns
- Test a target which causes less noise (1 only if variation +0.5%)
- Perform **GridSearchCV** to fine-tune model hyperparameters  
- Compare with **more advanced classifiers** (e.g., SVM, XGBoost)  
- **Enrich the dataset** with macroeconomic indicators, others technical indicators (non correlated), news sentiment analysis, etc...
