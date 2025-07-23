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
  - F1-score: **0.695**

- **Using selected features**:
  - ROC AUC: **0.80**
  - Precision*: **0.73**
  - Recall*: **0.73**
  - F1-score: **0.73**

> * Simple average between precision, recall and f1-score across both classes (`0 = down`, `1 = up`)

---

### 📉 Backtest results (confidence > 75%)

| Metric                             | Value        |
|-----------------------------------|--------------|
| **Overall cumulative return**     | **-18.52%**  |
| Initial capital (base 1.0)        | 1.0000       |
| Final capital                     | 0.8148       |
| Number of trades executed         | 322          |
| Max daily return                  | +3.62%       |
| Min daily return                  | -3.16%       |
| Peak capital value                | 1.0981       |
| Max performance                   | +9.8082%     |
| Lowest capital value              |  0.807       |
| Min performance                   | -19.3029 %   |

---

### ⏱️ Strategy performance over time

- **📈 Growth phase (25/04/2021 → 24/04/2024)**  
  → Capital increased from **1.0000** to **1.0981** → **+9.8082%**

- **📉 Decline phase (24/04/2024 → 15/07/2025)**  
  → Capital dropped to **0.807** → **-19.3029%** from the peak

These results show that the model has reasonable predictive power, but the trading strategy is **highly volatile** and struggles with **loss management**.

---

## 🔧 Areas for Improvement

- Add a **stop-loss mechanism** to limit drawdowns
- Test a target which causes less noise (1 only if variation +0.5%)
- Perform **GridSearchCV** to fine-tune model hyperparameters  
- Compare with **more advanced classifiers** (e.g., SVM, XGBoost)  
- **Enrich the dataset** with macroeconomic indicators, others technical indicators (non correlated), news sentiment analysis, etc...
