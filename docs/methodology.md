# Méthodologie

## Vue d'Ensemble

Le pipeline adopte une approche **multi-modèles** pour maximiser la robustesse des prévisions. Chaque pays est traité indépendamment, avec sélection automatique du meilleur modèle selon le R².

---

## 1. Prétraitement des Données

### Agrégation temporelle

Les données hebdomadaires brutes sont agrégées en **données mensuelles** (moyenne mobile) pour réduire le bruit et améliorer la stationnarité des séries.

### Feature Engineering

Les variables temporelles suivantes sont dérivées du dataset :
- Mois, trimestre, année
- Lag features : `TB_Cases_lag1`, `lag2`, `lag3`, `lag12`
- Rolling features : moyenne mobile 3 mois, 6 mois
- Variables exogènes : `GDP_Per_Capita`, `HIV_Prevalence`, `Healthcare_Index`

---

## 2. Tests de Stationnarité

Avant modélisation ARIMA/SARIMA, la stationnarité de chaque série est vérifiée :

| Test | Hypothèse nulle | Seuil p-value |
|------|----------------|---------------|
| **ADF** (Augmented Dickey-Fuller) | Série non-stationnaire | < 0.05 |
| **KPSS** (Kwiatkowski-Phillips-Schmidt-Shin) | Série stationnaire | > 0.05 |

En cas de non-stationnarité, une **différenciation d'ordre 1** (`d=1`) est appliquée.

---

## 3. Modèles Statistiques

### ARIMA(p, d, q)

Modèle autorégressif intégré à moyenne mobile. Les ordres sont sélectionnés automatiquement via `pmdarima.auto_arima` (critère AIC).

### SARIMA(p, d, q)(P, D, Q, s)

Extension saisonnière d'ARIMA avec période `s=12` (saisonnalité annuelle). Adapté à la cyclicité des épidémies tuberculineuses.

### SARIMAX

Version étendue de SARIMA intégrant des variables exogènes (`PIB`, `VIH`, `Healthcare_Index`) pour améliorer les prévisions à moyen terme.

---

## 4. Modèles Machine Learning

### XGBoost

- Gradient boosting avec régularisation L1/L2
- Hyperparamètres : `n_estimators=500`, `max_depth=6`, `learning_rate=0.05`
- Robuste aux outliers épidémiques

### LightGBM

- Gradient boosting optimisé pour les grandes datasets
- Hyperparamètres : `n_estimators=500`, `num_leaves=31`, `learning_rate=0.05`
- Temps d'entraînement réduit par rapport à XGBoost

---

## 5. Détection des Anomalies

Le pipeline utilise une approche **hybride IQR + Z-score** :

1. Calcul du Z-score pour chaque observation par pays
2. Flagging si `|Z| > 2.5`
3. Classification automatique :
   - **COVID-19** : anomalie entre mars 2020 et décembre 2021
   - **Spike épidémique** : valeur supérieure au 95ème percentile
   - **Anomalie normale** : autre

---

## 6. Évaluation

Les modèles sont évalués sur un **jeu de test** (20% des données, split temporel) avec les métriques suivantes :

| Métrique | Description |
|----------|-------------|
| **RMSE** | Root Mean Squared Error — pénalise les grandes erreurs |
| **MAE** | Mean Absolute Error — erreur absolue moyenne |
| **R²** | Coefficient de détermination — qualité globale du fit |

Le meilleur modèle par pays est sélectionné sur la base du **R² maximum**.

---

## 7. Prévisions

Les prévisions sont générées sur **12 et 24 mois** à partir du dernier point connu, avec :
- Valeur centrale (point forecast)
- Intervalles de confiance à 80% et 95% (modèles statistiques uniquement)
