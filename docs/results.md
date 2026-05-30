# Résultats

## Résumé des Performances

### Meilleures Performances par Pays

| Pays | Meilleur Modèle | R² | RMSE |
|------|----------------|-----|------|
| 🇮🇩 Indonesia | XGBoost | **0.9145** | 2 264 |
| 🇮🇳 India | XGBoost | **0.9073** | 10 305 |
| 🇵🇰 Pakistan | LightGBM | **0.8989** | 1 128 |
| 🇨🇩 DR Congo | LightGBM | **0.8322** | 1 065 |
| 🇲🇦 Morocco | XGBoost | **0.7817** | 62 |
| 🇵🇭 Philippines | LightGBM | **0.7392** | 1 284 |
| 🇪🇹 Ethiopia | LightGBM | **0.7217** | 2 929 |
| 🇳🇬 Nigeria | LightGBM | **0.7131** | 4 277 |
| 🇿🇦 South Africa | LightGBM | **0.6885** | 1 862 |
| 🇧🇩 Bangladesh | XGBoost | **0.6326** | 2 711 |
| 🇨🇳 China | LightGBM | **0.3230** | 8 522 |

**Modèle le plus performant globalement : LightGBM** (meilleur pour 7 pays sur 11)

---

## Comparaison des Modèles

| Modèle | Pays ⭐ (R² > 0.8) | Pays ⚡ (R² > 0.6) | Pays ⚠️ (R² < 0.6) |
|--------|------------------|------------------|------------------|
| XGBoost | India, Indonesia | Bangladesh, Morocco | — |
| LightGBM | Pakistan, DR Congo | Ethiopia, Nigeria, S. Africa, Philippines | China |
| SARIMA | — | Variable | Variable |
| SARIMAX | — | Variable | Variable |
| ARIMA | — | — | Variable |

---

## Anomalies Détectées

**Total : 45 anomalies** identifiées sur l'ensemble des pays et de la période.

| Type | Nombre | Période principale |
|------|--------|-------------------|
| Spike épidémique | 22 | Tout au long de la série |
| Anomalie normale | 16 | Distribué |
| COVID-19 | 7 | Mars 2020 – Décembre 2021 |

### Impact COVID-19

La pandémie de COVID-19 a causé une **chute artificielle des cas déclarés** entre 2020 et 2021, due à :
- Fermeture ou saturation des services de santé
- Réorientation des ressources vers le COVID
- Sous-déclaration des cas TB

Un rebond post-pandémique est observé dans la plupart des pays à partir de 2022.

---

## Interprétation Épidémiologique

### Tendances Long Terme

La charge tuberculeuse mondiale montre une **tendance décroissante** sur 2003–2026, attribuable aux programmes internationaux (DOTS, Stop TB Partnership, End TB Strategy).

### Facteurs Corrélés

| Variable | Corrélation avec TB_Cases | Interprétation |
|----------|--------------------------|----------------|
| HIV_Prevalence | ➕ Forte | Co-infection fragilise l'immunité |
| GDP_Per_Capita | ➖ Négative | Revenus élevés → meilleures infrastructures |
| Healthcare_Index | ➖ Négative | Accès aux soins réduit la transmission |
| Vaccination_Rate | ➖ Faible | BCG protège partiellement |

### Performance des Modèles

- **SARIMA** : excellent pour capturer la saisonnalité épidémique (s=12)
- **LightGBM / XGBoost** : supérieurs sur les données bruitées, robustes aux outliers COVID
- **SARIMAX** : amélioration marginale avec variables exogènes (PIB, VIH)

---

## Prévisions 2026–2028

Les modèles projettent, pour la majorité des pays :

- **Poursuite de la tendance décroissante** dans les pays à revenu intermédiaire (India, Indonesia, Morocco)
- **Stagnation ou légère hausse** dans les pays à système de santé fragile (DR Congo, Ethiopia, Nigeria)
- **Incertitude élevée** pour la Chine (R²=0.32), nécessitant des données complémentaires

!!! note "Intervalles de confiance"
    Les prévisions SARIMA/SARIMAX incluent des intervalles de confiance à 80% et 95%.
    L'incertitude croît avec l'horizon temporel — les prévisions à 24 mois sont à interpréter avec prudence.

---

## Fichiers de Résultats

| Fichier | Contenu |
|---------|---------|
| `outputs/global_metrics.xlsx` | Métriques complètes (RMSE, MAE, R²) pour tous les modèles × pays |
| `outputs/global_forecasts.xlsx` | Prévisions mensuelles 12 et 24 mois par pays |
| `outputs/anomalies.xlsx` | Liste des anomalies avec type, date, pays et valeur |
| `outputs/models/*.pkl` | Modèles sérialisés pour déploiement |
