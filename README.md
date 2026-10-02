# McDonald's Menu 2026 — Data Analysis & Visualization

Projet de Data Analysis réalisé dans le cadre de la **Cohorte 2 — Data Science de l'Akieni Academy**.

## 1. Contexte

L'équipe Data Analytics reçoit un jeu de données portant sur le **menu McDonald's 2026**.

La mission consiste à explorer la structure du menu, évaluer la qualité des données, analyser les prix et les informations nutritionnelles, puis construire des visualisations permettant de mettre en évidence les tendances, différences entre catégories et relations entre variables.

Le projet applique une démarche de Data Analyst :

> **Comprendre → Auditer → Investiguer → Décider → Analyser → Visualiser → Interpréter**

---

## 2. Problématique

> **Que nous apprennent les données du menu McDonald's 2026 sur la relation entre le prix, les calories et les caractéristiques nutritionnelles des produits ?**

---

## 3. Objectifs

Le projet vise à :

* comprendre la structure et le contenu du dataset ;
* évaluer sa qualité : types, valeurs manquantes, doublons, valeurs atypiques et incohérences ;
* décrire la composition du menu et ses catégories ;
* analyser les distributions de prix et de calories ;
* explorer les variables nutritionnelles disponibles ;
* étudier les relations entre prix, calories et autres variables numériques ;
* identifier les produits atypiques et distinguer anomalie potentielle et observation réelle ;
* créer des indicateurs dérivés lorsque cela est justifié ;
* construire une narration visuelle claire ;
* formuler une synthèse fondée sur les résultats réellement calculés.

---

## 4. Questions d'analyse

| Axe               | Question principale                                                                                |
| ----------------- | -------------------------------------------------------------------------------------------------- |
| **Compréhension** | Combien de produits ? Quelles catégories ? Comment le menu est-il réparti ?                        |
| **Qualité**       | Les données sont-elles complètes, cohérentes et correctement structurées ?                         |
| **Prix**          | Comment les prix sont-ils distribués et quelles différences observe-t-on entre catégories ?        |
| **Calories**      | Comment les calories sont-elles distribuées et quelles différences observe-t-on entre catégories ? |
| **Nutrition**     | Quelles variables nutritionnelles sont disponibles et comment se répartissent-elles ?              |
| **Relations**     | Existe-t-il une association entre prix, calories et variables nutritionnelles ?                    |
| **Atypiques**     | Quels produits s'écartent fortement du comportement général ?                                      |
| **Visualisation** | Quels graphiques permettent de répondre le plus clairement aux questions ?                         |
| **Synthèse**      | Quels constats peut-on retenir sans dépasser ce que les données permettent d'affirmer ?            |

---

## 5. Démarche analytique

L'analyse est réalisée progressivement :

```text
Données brutes
      ↓
Data Understanding
      ↓
Data Quality Audit
      ↓
Investigation des observations suspectes
      ↓
Data Cleaning & Decision
      ↓
Validation
      ↓
EDA
      ↓
Data Visualization
      ↓
Interprétation
      ↓
Synthèse
```

Une observation suspecte n'est pas automatiquement corrigée. Toute décision de nettoyage doit être précédée d'une inspection de la donnée, d'une vérification de sa cohérence métier et, lorsque cela est possible, d'un contrôle de sa source.

---

## 6. Data Quality

L'audit porte notamment sur :

* les dimensions et types de données ;
* les valeurs manquantes ;
* les doublons ;
* l'unicité de `item_id` ;
* les valeurs négatives et nulles ;
* les chaînes vides ;
* les variables booléennes ;
* les structures JSON ;
* les variables calculées ;
* les règles de cohérence nutritionnelle.

Exemples de contraintes nutritionnelles :

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

Certaines relations sont également contrôlées :

```text
saturated_fat_g <= total_fat_g
trans_fat_g <= total_fat_g
sugars_g <= total_carbs_g
```

Les règles détaillées sont documentées dans `docs/data_quality_rules.md`.

---

## 7. Analyse et visualisation

L'EDA porte principalement sur :

* la composition du menu ;
* les catégories ;
* les prix ;
* les calories ;
* les variables nutritionnelles ;
* les relations entre variables ;
* les observations atypiques.

Les visualisations peuvent inclure des histogrammes, boxplots, barplots, scatterplots et heatmaps.

Chaque graphique doit répondre à une question analytique et être accompagné d'une interprétation proportionnée aux données.

> **Une association observée entre deux variables ne constitue pas automatiquement une relation de causalité.**

---

## 8. Source des données

**Source :** Kaggle — *McDonald's Menu Prices and Nutrition 2026*

Le fichier CSV fourni constitue la **source de vérité** pour les noms de colonnes, les types, les valeurs et la structure du dataset.

Les variables utilisées dans l'analyse sont donc vérifiées directement à partir du fichier fourni, sans supposer l'existence de variables absentes du dataset.

---

## 9. Notebook principal

L'ensemble du projet est centralisé dans un notebook unique :

```text
notebooks/
└── mcdonalds_menu_2026_data_analysis.ipynb
```

Il est organisé selon les étapes suivantes :

```text
01. Chargement des données
02. Data Understanding
03. Data Quality Audit
04. Validation des règles métier
05. Data Cleaning & Decision
06. Validation après nettoyage
07. Exploratory Data Analysis
08. Data Visualization
09. Interprétation
10. Synthèse finale
```

---

## 10. Structure du repository

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

## 11. Documentation

Le dossier `docs/` contient les éléments complémentaires du projet :

| Fichier                 | Contenu                                  |
| ----------------------- | ---------------------------------------- |
| `cahier_des_charges.md` | Contexte, problématique et objectifs     |
| `data_dictionary.md`    | Description des variables                |
| `data_quality_rules.md` | Règles de contrôle qualité               |
| `cleaning_decisions.md` | Décisions et justifications de nettoyage |

---

## 12. Prérequis

### Technologies

* Python 3
* Jupyter Notebook
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Git
* GitHub

### Installation

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

## 13. Objectif pédagogique

Ce projet constitue une mise en pratique du parcours **Data Science — Cohorte 2 de l'Akieni Academy**.

L'objectif est de développer une analyse structurée, reproductible et documentée, en accordant autant d'importance au **raisonnement analytique** qu'au code et aux visualisations.

---

## 14. Statut

**Projet en cours de développement.**

Les différentes étapes de l'analyse sont progressivement complétées et documentées dans le repository.

---

## Auteur

**Trésor KITWANDA**

**Akieni Academy — Cohorte 2 Data Science**

Projet Freestyle — EDA & Data Visualization
