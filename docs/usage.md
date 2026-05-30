# Utilisation

## Exécution du Pipeline Complet

Le pipeline est structuré en **15 sections** dans le notebook `collab.ipynb`. L'exécution séquentielle de toutes les cellules suffit pour obtenir l'ensemble des résultats.

---

## Sections du Notebook

| Section | Titre | Description |
|---------|-------|-------------|
| 1 | Installation des bibliothèques | Installation automatique des dépendances |
| 2 | Importation des modules | Chargement des librairies Python |
| 3 | Connexion Google Drive | Montage du drive et chargement du dataset |
| 4 | Exploration des données | Statistiques descriptives, valeurs manquantes |
| 5 | Prétraitement | Agrégation mensuelle, nettoyage, features temporelles |
| 6 | Analyse EDA | Tendances, saisonnalité, corrélations |
| 7 | Tests de stationnarité | ADF, KPSS, ACF/PACF |
| 8 | Modèles ARIMA | Entraînement et évaluation ARIMA par pays |
| 9 | Modèles SARIMA | Capture de la saisonnalité annuelle (s=12) |
| 10 | Modèles SARIMAX | Intégration des variables exogènes |
| 11 | Modèles XGBoost | Feature engineering + gradient boosting |
| 12 | Modèles LightGBM | Entraînement LightGBM par pays |
| 13 | Comparaison des modèles | Métriques globales : RMSE, MAE, R² |
| 14 | Détection des anomalies | IQR + Z-score, classification COVID/spike |
| 15 | Résumé final | Rapport consolidé + génération des outputs |

---

## Outputs Générés

Après exécution complète, les fichiers suivants sont disponibles dans `outputs/` :

```
outputs/
├── global_metrics.xlsx       # RMSE, MAE, R² pour tous les modèles × pays
├── global_forecasts.xlsx     # Prévisions 12 et 24 mois par pays
├── anomalies.xlsx            # Anomalies détectées avec type et date
├── models/
│   ├── xgb_India.pkl
│   ├── lgb_India.pkl
│   └── ...                   # 1 modèle .pkl par algorithme × pays
└── *.png                     # Figures de séries, prévisions, comparaisons
```

---

## Lancer le Dashboard Streamlit

Le notebook génère un fichier `app.py` dans `/content/`. Pour le lancer :

```bash
# Depuis un terminal local (après téléchargement de app.py)
streamlit run app.py
```

Dans Colab, le dashboard est exposé via un tunnel **ngrok** (Section 14 du notebook).

---

## Paramètres Configurables

Dans le notebook, les paramètres globaux sont définis en haut de chaque section :

```python
# Pays à analyser
PAYS_CIBLES = [
    'India', 'China', 'Indonesia', 'Pakistan', 'Nigeria',
    'Bangladesh', 'South Africa', 'Philippines',
    'DR Congo', 'Ethiopia', 'Morocco'
]

# Horizons de prévision (en mois)
HORIZON_12 = 12
HORIZON_24 = 24

# Seuil d'anomalie (Z-score)
SEUIL_ZSCORE = 2.5
```
