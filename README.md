# Project Journey
Initially, I built a model using all raw features and a target very sensitive to micro-variations, which led to noisy predictions and poor strategy performance.
After noticing a strange phenomenon—where the model was right statistically, went up for 2 years (+11%) then suddendly drop and lost money (-17,14%)— I analyzed the predictions and trading behavior. I then iteratively improved the approach by:
- Creating a cleaner target variable (only predicting class 1 if price increase > +0.5%) to reduce noise
- Using feature selection to remove irrelevant or redundant variables
- Running a grid search to tune two key parameters:
            -The confidence threshold on the model's probability
            -A stop-loss rule: exit trade if the cumulative return over 2 consecutive days falls below -2%

This process helped transform a fragile strategy into a profitable one in appearance with controlled drawdowns.
## Disclaimer ⚠️
This project was carried out as part of a learning process: my goal was to understand how to build, test, and improve a trading strategy using machine learning.
While the final results show an apparent performance of around **+7,11%**, I fully acknowledge that this figure does **not necessarily reflect real-world execution**. It is a backtest on historical data, with all the limitations that come with it (simplified assumptions, possible overfitting, no transaction costs or slippage, etc.).
I don’t claim to have found a reliable strategy — this repository documents my thinking process, iterations, and key takeaways. The main objective is to **develop analytical rigor**, by exploring the limitations of the model and seeking continuous improvement.

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
  - ROC AUC: **0.72**
  - Precision*: **0.65**
  - Recall*: **0.635**
  - F1-score: **0.64**

- **Using selected features**:
  - ROC AUC: **0.78**
  - Precision*: **0.705**
  - Recall*: **0.705**
  - F1-score: **0.705**

> * Simple average between precision, recall and f1-score across both classes (`0 = down`, `1 = up`)

---

### 📉 Backtest results (confidence > 75% and stoploss at -2% cumulated for 2 consecutive days)

| Metric                             | Value        |
|-----------------------------------|--------------|
| **Overall cumulative return**     | **+7,11%**  |
| Initial capital (base 1.0)        | 1.0000       |
| Final capital                     | 1,0711       |
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
