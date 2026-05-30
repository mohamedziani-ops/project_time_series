# 🦠 TB Global Forecasting — Pipeline de Séries Temporelles

Pipeline professionnel d'analyse et de prévision épidémiologique de la tuberculose mondiale, couvrant **11 pays à forte charge**, sur la période **2003–2026**.

[![Python](https://img.shields.io/badge/Python-3.9%2B-blue)](https://www.python.org/)
[![Google Colab](https://img.shields.io/badge/Google%20Colab-Compatible-orange)](https://colab.research.google.com/)
[![MkDocs](https://img.shields.io/badge/Docs-MkDocs-green)](https://www.mkdocs.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow)](LICENSE)

---

## 📋 Description

Ce projet implémente un **pipeline complet de séries temporelles** pour modéliser et prévoir les cas de tuberculose (TB) à l'échelle mondiale. Il combine des approches statistiques classiques (ARIMA, SARIMA, SARIMAX) et des modèles de machine learning (XGBoost, LightGBM), avec détection automatique des anomalies et dashboard interactif Streamlit.

---

## 🌍 Pays Étudiés

| Pays | Code ISO | Meilleur modèle | R² |
|------|----------|-----------------|-----|
| India | IND | XGBoost | 0.9073 |
| Indonesia | IDN | XGBoost | 0.9145 |
| Pakistan | PAK | LightGBM | 0.8989 |
| DR Congo | COD | LightGBM | 0.8322 |
| Ethiopia | ETH | LightGBM | 0.7217 |
| Morocco | MAR | XGBoost | 0.7817 |
| Philippines | PHL | LightGBM | 0.7392 |
| South Africa | ZAF | LightGBM | 0.6885 |
| Nigeria | NGA | LightGBM | 0.7131 |
| Bangladesh | BGD | XGBoost | 0.6326 |
| China | CHN | LightGBM | 0.3230 |

---

## 📁 Structure du Projet

```
project_time_series/
│
├── TB_Global_Weekly_Dataset.xlsx   # Dataset source (239 323 lignes × 15 colonnes)
├── collab.ipynb                    # Notebook Google Colab principal
│
├── README.md
├── requirements.txt
├── .gitignore
├── mkdocs.yml
│
└── docs/
    ├── index.md
    ├── installation.md
    ├── usage.md
    ├── methodology.md
    └── results.md
```

---

## ⚡ Démarrage Rapide

### 1. Cloner le dépôt

```bash
git clone https://github.com/votre-utilisateur/project_time_series.git
cd project_time_series
```

### 2. Installer les dépendances

```bash
pip install -r requirements.txt
```

### 3. Exécuter sur Google Colab

Ouvrir `collab.ipynb` dans [Google Colab](https://colab.research.google.com/), monter Google Drive, et exécuter toutes les cellules.

### 4. Lancer la documentation locale

```bash
mkdocs serve
```

---

## 🤖 Modèles Implémentés

- **ARIMA** — Modélisation des tendances non-saisonnières
- **SARIMA** — Capture de la saisonnalité annuelle (s=12)
- **SARIMAX** — Intégration des variables exogènes (PIB, VIH, indice de santé)
- **XGBoost** — Gradient boosting robuste aux outliers
- **LightGBM** — Gradient boosting rapide sur données bruitées

---

## 📊 Variables du Dataset

| Variable | Description |
|----------|-------------|
| `TB_Cases` | Nombre de cas hebdomadaires (cible) |
| `TB_Deaths` | Nombre de décès |
| `TB_Incidence_Rate` | Taux d'incidence pour 100 000 hab. |
| `Healthcare_Index` | Indice d'accès aux soins |
| `Vaccination_Rate` | Taux de vaccination BCG |
| `GDP_Per_Capita` | PIB par habitant (USD) |
| `Urbanization_Rate` | Taux d'urbanisation |
| `HIV_Prevalence` | Prévalence VIH (%) |

---

## 🚨 Détection des Anomalies

Le pipeline identifie automatiquement 3 types d'anomalies :
- **Spike épidémique** (22 détectées)
- **Anomalie normale** (16 détectées)
- **Impact COVID-19** (7 détectées, période 2020–2021)

---

## 📈 Outputs Générés

Après exécution complète du notebook :

```
outputs/
├── global_metrics.xlsx      # Métriques de performance de tous les modèles
├── global_forecasts.xlsx    # Prévisions 12 et 24 mois par pays
├── anomalies.xlsx           # Anomalies détectées
├── models/                  # Modèles sérialisés (.pkl)
└── *.png                    # Figures et visualisations
```

---

## 🧰 Technologies

- **Python 3.9+**
- `pandas`, `numpy` — manipulation des données
- `statsmodels`, `pmdarima` — modèles statistiques
- `xgboost`, `lightgbm` — machine learning
- `plotly`, `matplotlib`, `seaborn` — visualisation
- `streamlit` — dashboard interactif
- `scikit-learn` — métriques et prétraitement

---

## 📄 Licence

Ce projet est distribué sous licence MIT. Voir le fichier `LICENSE` pour plus de détails.

---

## 👤 Auteur

**Mohamed Ziani et Hamdi Maria**  
Projet de forecasting épidémiologique — 2026
