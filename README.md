# mcdonalds-menu-2026-data-analysis
Data analysis and visualization of the McDonald's Menu 2026 dataset, focusing on price, calories, nutrition, data quality, and exploratory analysis.

# McDonald's Menu 2026 — Data Analysis & Visualization

## Présentation

Ce repository présente un projet d'analyse de données réalisé dans le cadre de la **Cohorte 2 — Data Science de l'Akieni Academy**.

Le projet porte sur un dataset consacré au **menu McDonald's 2026**. Il vise à analyser les relations entre le prix, les calories et les caractéristiques nutritionnelles des produits.

L'objectif est de mettre en pratique une démarche complète de **Data Analyst**, depuis la compréhension et l'audit des données jusqu'à l'analyse exploratoire, la visualisation et l'interprétation des résultats.

---

## Contexte du projet

**Programme :** Akieni Academy
**Parcours :** Data Science
**Cohorte :** Cohorte 2
**Projet :** Projet Freestyle — EDA & Data Visualization

Ce projet permet de mettre en pratique plusieurs compétences acquises au cours du parcours :

* Python
* Pandas
* NumPy
* Data Quality
* Data Cleaning
* Exploratory Data Analysis (EDA)
* Data Visualization
* Interprétation des données

---

## Problématique

> **Existe-t-il des relations observables entre le prix, les calories et les caractéristiques nutritionnelles des produits du menu ?**

Cette problématique est étudiée à travers plusieurs axes :

* distribution des prix ;
* distribution des calories ;
* répartition des produits par catégorie ;
* relation entre prix et calories ;
* relation entre prix et protéines ;
* comportement des variables nutritionnelles ;
* identification des observations atypiques.

---

## Démarche analytique

Le projet suit une démarche structurée :

```text
Données brutes
      ↓
Data Understanding
      ↓
Data Quality Audit
      ↓
Identification des observations à investiguer
      ↓
Data Cleaning & Decision
      ↓
Validation après nettoyage
      ↓
Exploratory Data Analysis
      ↓
Data Visualization
      ↓
Interprétation
      ↓
Synthèse
```

Cette organisation permet de distinguer clairement :

* les constats issus des données ;
* les observations nécessitant une investigation ;
* les décisions de nettoyage ;
* les résultats de l'analyse.

---

## Data Understanding & Data Quality Audit

Avant toute modification des données, un audit qualité est réalisé.

Les contrôles portent notamment sur :

| Domaine             | Contrôle                     |
| ------------------- | ---------------------------- |
| Structure           | Dimensions du dataset        |
| Types               | Types des variables          |
| Complétude          | Valeurs manquantes           |
| Unicité             | Doublons                     |
| Identifiant         | `item_id`                    |
| Prix                | Valeurs `<= 0`               |
| Calories            | Valeurs `<= 0`               |
| Nutrition           | Valeurs négatives            |
| Texte               | Chaînes vides                |
| Booléens            | Modalités                    |
| JSON                | Structure de `price_history` |
| Variables calculées | Cohérence des formules       |

### Principe de qualité des données

> **L'absence de valeurs manquantes ne signifie pas nécessairement que les données sont de bonne qualité.**

Une donnée peut être complète tout en présentant une valeur incompatible avec sa signification métier, une incohérence entre plusieurs variables ou une erreur dans une variable calculée.

L'audit permet donc d'identifier les points nécessitant une investigation avant de procéder au nettoyage.

---

## Validation des données nutritionnelles

Les variables nutritionnelles sont confrontées à des règles métier.

Exemples :

```text
total_fat_g >= 0
saturated_fat_g >= 0
trans_fat_g >= 0
dietary_fiber_g >= 0
sugars_g >= 0
total_carbs_g >= 0
protein_g >= 0
calories >= 0
```

Certaines relations entre variables sont également contrôlées :

```text
saturated_fat_g <= total_fat_g
trans_fat_g <= total_fat_g
sugars_g <= total_carbs_g
```

Ces règles permettent d'identifier les observations qui doivent être examinées.

Une violation de règle ne conduit pas automatiquement à une correction.

---

## Data Cleaning & Decision

La démarche de nettoyage repose sur le principe suivant :

```text
Voir la ligne concernée
        ↓
Comprendre le produit
        ↓
Vérifier la cohérence métier
        ↓
Examiner la source si disponible
        ↓
Prendre une décision
        ↓
Appliquer le traitement
        ↓
Vérifier après nettoyage
        ↓
Documenter la décision
```

L'objectif est d'éviter les corrections automatiques qui pourraient modifier les données sans justification.

Lorsque cela est nécessaire, les valeurs originales sont conservées afin de garantir la traçabilité des transformations.

---

## Exploratory Data Analysis

L'analyse exploratoire cherche notamment à répondre aux questions suivantes :

* Comment les prix sont-ils distribués ?
* Comment les calories sont-elles distribuées ?
* Comment les produits sont-ils répartis entre les catégories ?
* Existe-t-il une relation entre prix et calories ?
* Existe-t-il une relation entre prix et protéines ?
* Quelles variables nutritionnelles sont associées aux calories ?
* Quels produits présentent des comportements atypiques ?

---

## Data Visualization

Les visualisations sont utilisées pour faciliter l'exploration et l'interprétation des données.

Les graphiques peuvent notamment inclure :

* histogrammes ;
* boxplots ;
* barplots ;
* scatterplots ;
* heatmaps ;
* comparaisons entre catégories.

Chaque visualisation est associée à une question analytique.

> **Un graphique doit apporter une information utile à l'analyse et non être produit uniquement pour représenter les données.**

---

## Notebook principal

L'ensemble de la démarche est centralisé dans un notebook unique :

```text
notebooks/
└── mcdonalds_menu_2026_data_analysis.ipynb
```

Le notebook suit l'ordre logique :

```text
1. Data Loading
2. Data Understanding
3. Data Quality Audit
4. Validation des règles métier
5. Data Cleaning & Decision
6. Validation après nettoyage
7. Exploratory Data Analysis
8. Data Visualization
9. Interprétation
10. Conclusion
```

Cette organisation permet de suivre l'intégralité du raisonnement analytique dans un même document.

---

## Structure du repository

```text
mcdonalds-menu-2026-data-analysis/
│
├── data/
│   └── README.md
│
├── notebooks/
│   └── mcdonalds_menu_2026_data_analysis.ipynb
│
├── docs/
│   ├── cahier_des_charges.md
│   ├── data_dictionary.md
│   ├── data_quality_rules.md
│   └── cleaning_decisions.md
│
├── outputs/
│   ├── figures/
│   └── tables/
│
├── .gitignore
├── README.md
├── requirements.txt
└── LICENSE
```

---

## Documentation

Le dossier `docs/` contient les éléments permettant de comprendre le projet au-delà du code :

| Document                | Contenu                                         |
| ----------------------- | ----------------------------------------------- |
| `cahier_des_charges.md` | Contexte, objectifs, problématique et périmètre |
| `data_dictionary.md`    | Description et signification des variables      |
| `data_quality_rules.md` | Règles de validation des données                |
| `cleaning_decisions.md` | Décisions et justifications liées au nettoyage  |

---

## Technologies utilisées

* Python 3
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Jupyter Notebook
* Git
* GitHub

---

## Reproduire le projet

Cloner le repository :

```bash
git clone <URL_DU_REPOSITORY>
```

Créer un environnement Python :

```bash
python -m venv .venv
```

Activer l'environnement sous Windows :

```bash
.venv\Scripts\activate
```

Installer les dépendances :

```bash
pip install -r requirements.txt
```

Lancer Jupyter :

```bash
jupyter notebook
```

Puis ouvrir :

```text
notebooks/mcdonalds_menu_2026_data_analysis.ipynb
```

---

## Objectif pédagogique

Ce projet a pour objectif de mettre en pratique la démarche d'un **Data Analyst** dans le cadre de la **Cohorte 2 — Data Science de l'Akieni Academy**.

L'accent est mis autant sur le raisonnement que sur le code :

> **Comprendre → Auditer → Investiguer → Décider → Nettoyer → Vérifier → Analyser → Visualiser → Interpréter**

Cette démarche vise à produire une analyse :

* compréhensible ;
* reproductible ;
* documentée ;
* justifiable ;
* cohérente avec les règles métier.

---

## Statut du projet

**Projet en cours de développement.**

Les différentes étapes de l'analyse sont progressivement complétées et documentées dans le repository.

---

## Auteur

**Trésor KITWANDA**

Data Analyst — Data Science Learner

**Akieni Academy — Cohorte 2 Data Science**

Projet Freestyle — EDA & Data Visualization
