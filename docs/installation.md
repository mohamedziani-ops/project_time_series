# Installation

## Prérequis

- Python **3.9 ou supérieur**
- Compte **Google Drive** (pour l'exécution Colab)
- Git

---

## Option 1 — Google Colab (recommandé)

1. Uploader le projet sur Google Drive dans `MyDrive/project_time_series/`
2. Ouvrir `collab.ipynb` via [Google Colab](https://colab.research.google.com/)
3. Exécuter la **Section 1** du notebook — toutes les dépendances sont installées automatiquement :

```python
packages = [
    'statsmodels', 'pmdarima', 'xgboost', 'lightgbm',
    'plotly', 'kaleido', 'openpyxl', 'tqdm',
    'streamlit', 'scikit-learn'
]
```

---

## Option 2 — Installation Locale

### 1. Cloner le dépôt

```bash
git clone https://github.com/votre-utilisateur/project_time_series.git
cd project_time_series
```

### 2. Créer un environnement virtuel

```bash
python -m venv .venv
source .venv/bin/activate      # Linux / macOS
.venv\Scripts\activate         # Windows
```

### 3. Installer les dépendances

```bash
pip install -r requirements.txt
```

### 4. Vérifier l'installation

```bash
python -c "import xgboost, lightgbm, statsmodels, pmdarima; print('OK')"
```

---

## Installation de la Documentation

Pour générer et servir la documentation localement :

```bash
pip install mkdocs mkdocs-material
mkdocs serve
```

Accéder ensuite à [http://127.0.0.1:8000](http://127.0.0.1:8000).

Pour compiler en HTML statique :

```bash
mkdocs build
```

---

## Structure des Fichiers Attendue sur Google Drive

```
MyDrive/
└── project_time_series/
    ├── TB_Global_Weekly_Dataset.xlsx    ← requis
    ├── collab.ipynb
    └── outputs/                         ← créé automatiquement
```

!!! warning "Chemin Google Drive"
    Le notebook suppose que le fichier dataset est placé exactement à :
    `/content/drive/MyDrive/project_time_series/TB_Global_Weekly_Dataset.xlsx`
