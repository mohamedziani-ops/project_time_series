# 🦠 TB Global Forecasting

Bienvenue dans la documentation du **pipeline de forecasting épidémiologique de la tuberculose mondiale**.

---

## Présentation

Ce projet propose une solution complète de **modélisation et prévision des séries temporelles** appliquée à la tuberculose (TB), l'une des maladies infectieuses les plus meurtrières au monde.

Le pipeline couvre **11 pays à forte charge tuberculeuse** sur la période **2003–2026**, avec des données hebdomadaires issues d'un dataset synthétique aligné sur les statistiques OMS.

---

## Fonctionnalités Principales

- **Analyse exploratoire** des tendances et de la saisonnalité par pays
- **Modélisation statistique** : ARIMA, SARIMA, SARIMAX
- **Machine Learning** : XGBoost, LightGBM
- **Détection automatique des anomalies** (COVID-19, spikes épidémiques)
- **Prévisions 12 et 24 mois** avec intervalles de confiance
- **Dashboard interactif** Streamlit
- **Export automatique** des résultats (Excel, figures, modèles .pkl)

---

## Pays Couverts

> India · China · Indonesia · Pakistan · Nigeria · Bangladesh · South Africa · Philippines · DR Congo · Ethiopia · Morocco

---

## Navigation

| Section | Description |
|---------|-------------|
| [Installation](installation.md) | Prérequis et mise en place de l'environnement |
| [Utilisation](usage.md) | Guide d'exécution du pipeline |
| [Méthodologie](methodology.md) | Approches statistiques et ML utilisées |
| [Résultats](results.md) | Performances des modèles et conclusions |

---

!!! info "Exécution recommandée"
    Ce projet est optimisé pour **Google Colab**. L'exécution locale est possible mais nécessite une configuration GPU pour les modèles ML sur les 11 pays simultanément.
