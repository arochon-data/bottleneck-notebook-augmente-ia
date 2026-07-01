# 🍷 BottleNeck — Notebook P6 augmenté par l'IA

> Fiabilisation des données d'un caviste en ligne : validation déclarative (Pandera) et détection d'anomalies multivariées (Isolation Forest).

Amélioration **critique et documentée** d'un notebook d'analyse de stock, réalisée dans le cadre de ma formation **Business Intelligence Analyst** (OpenClassrooms). Le notebook reprend l'intégralité du projet initial et y intègre des améliorations issues d'une veille technologique, avec un usage de l'IA testé et vérifié.

📊 **[Portfolio complet](https://arochon-data.github.io/portfolio/)** · 💼 [LinkedIn](https://www.linkedin.com/in/antoine-rochon-8804a41/fr/)

---

## 🎯 Contexte & besoin

BottleNeck (marchand de vin en ligne) produit chaque mois un reporting de pilotage (stock, ventes, marge) à partir de deux systèmes hétérogènes : un **ERP** et une **plateforme web**, reliés par une table de liaison. Le contrôle qualité, qui conditionne la fiabilité de tous les indicateurs, était **manuel, au cas par cas et non rejouable**.

**Objectif :** transformer ce notebook ponctuel en un livrable fiable, reproductible et documenté, où la qualité des données est garantie **en amont** du calcul des indicateurs.

## 🚀 Améliorations apportées

| # | Amélioration | Ce que ça remplace / complète |
|---|---|---|
| 1 | **Validation déclarative (Pandera)** | Les ~20 contrôles manuels non rejouables → un schéma de règles auditable par fichier + un rapport lisible pour les métiers |
| 2 | **Détection d'anomalies multivariée (Isolation Forest)** | Complète (sans remplacer) les méthodes univariées Z-score / IQR pour capter les combinaisons rares prix × marge × ventes |
| 3 | **Reproductibilité** | Graine fixée (`SEED = 42`), jointures contrôlées (`validate=`), environnement figé, procédure *Restart & Run All* |

## 📈 Résultats (POC avant / après)

- **Code de contrôle divisé par ~2** (79 lignes / 17 cellules → 34 lignes / 1 schéma)
- **100 % des anomalies connues re-détectées**, avec un rapport interprétable **sans Python**
- **6 anomalies métier** révélées par la détection multivariée, invisibles à l'approche univariée (dead stock à déréférencer, prix d'achat à renégocier)
- Exécution reproductible en **moins de 5 secondes**

## 🧭 Choix techniques (issus de la veille)

- **Pandera plutôt que Great Expectations** — 12 dépendances contre 107 : adapté à un analyste seul sur notebook, sans infrastructure lourde (arbitrage de sobriété assumé).
- **Isolation Forest en complément du Z-score/IQR** — on conserve les contrôles univariés interprétables et on ajoute une couche multivariée ; paramètre `contamination` calibré par analyse de sensibilité.

## 🗂️ Contenu du dépôt

| Fichier | Description |
|---|---|
| `Rochon_Antoine_notebook_augmente.ipynb` | Notebook complet (analyse P6 + améliorations 🆕) |
| `requirements.txt` | Versions exactes des dépendances |
| `README.md` | Ce fichier |

> ℹ️ Les fichiers de données sources (`erp.xlsx`, `web.xlsx`, `liaison.xlsx`) ne sont pas inclus dans ce dépôt public.

## ⚙️ Installation & exécution

```bash
pip install -r requirements.txt
jupyter notebook Rochon_Antoine_notebook_augmente.ipynb
# puis : Kernel > Restart & Run All
```

## 🛠️ Stack technique

`Python` · `pandas` · `pandera` · `scikit-learn` · `plotly` · `matplotlib` · `seaborn` · `Jupyter`

## ⚠️ Limites & prochaines pistes

- Dataset réduit (~800 lignes) : Isolation Forest reste un **complément illustratif**.
- Le score d'anomalie est moins interprétable qu'un seuil explicite → maintien des contrôles univariés en parallèle.
- **Pistes :** industrialiser la validation à chaque export mensuel, suivre la dérive des anomalies dans le temps.

---

*Projet réalisé dans le cadre du parcours Business Intelligence Analyst — OpenClassrooms.*
