# TTE-Market-Direction-Prediction-LogisticRegression
Dans ce projet, j'explore l'utilisation de la régression logistique pour prédire la direction du marché à court terme, en se basant sur les données historiques de TotalEnergies (TTE). Il combine **analyse technique**, **indicateurs financiers** et **modélisation machine learning**, avec un focus sur l’explicabilité et un début de stratégie de trading.

## 📌 Objectifs

- Utiliser les données historiques de TTE depuis 2000
- Ajouter des indicateurs techniques classiques (MA, RSI, Sharpe Ratio…)
- Construire une variable cible (hausse ou baisse du cours)
- Entraîner un modèle de régression logistique avec validation temporelle
- Comparer les résultats avec features brutes et épurées
- Simuler une stratégie de trading filtrée par confiance (> 75%)

## Méthodologie

- Librairies : `pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn`, `yfinance`
- Modèle : `LogisticRegression` de scikit-learn
- Split temporel : `TimeSeriesSplit` (préserve la causalité)
- Visualisation : ROC curve, Matrice de confusion, Coefficients du modèle
- Librairies : `pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn`, `yfinance`

## 🧪 Résultats

### 🎯 Performances du modèle

- **Avec features brutes** :
  - ROC AUC : **0.76**
  - Précision* : **0.705**
  - Rappel* : **0.70**

- **Avec features épurées** :
  - ROC AUC : **0.80**
  - Précision* : **0.72**
  - Rappel* : **0.72**

> * Moyenne simple entre précision et rappel pour les deux classes (`0 = baisse`, `1 = hausse`)

---

### 📉 Résultats du backtest (confiance > 75 %)

| Indicateur                         | Valeur       |
|-----------------------------------|--------------|
| **Performance globale cumulée**   | **-17.51 %** |
| Capital initial (base 1.0)        | 1.0000       |
| Capital final                     | 0.8249       |
| Nombre de trades exécutés         | 316          |
| Rendement journalier max          | +3.62 %      |
| Rendement journalier min          | -3.16 %      |
| Capital maximum atteint           | 1.1114       |
| Performance maximale              | +11.14 %     |
| Capital minimum atteint           | 0.8175       |
| Performance minimale              | -18.25 %     |

---

### Comportement de la stratégie dans le temps

- **📈 Phase de hausse (25/04/2021 → 24/04/2024)**  
  → Le capital monte de **1.0000** à **1.1114** → **+11.14 %**

- **📉 Phase de baisse (24/04/2024 → 15/07/2025)**  
  → Le capital chute à **0.8249** → **-17.14 %** depuis le pic

---

Ces résultats montrent que le modèle est relativement robuste en phase de prédiction, mais ma stratégie de trading est très volatile et gère mal les pertes 


## Idées d'amélioration

- Inclure un **stop-loss** dans ma stratégie pour limiter les pertes
- Faire un **GridSearchCV** pour optimiser les hyperparamètres du modèle
- Comparer avec des **modèles de classfication plus performants** (SVM, XGBoost, etc.)
- **Enrichir le dataset** avec des données macroéconomiques, des analyses de sentiments... 
