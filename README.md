# McDonald's Menu 2026 — Data Analysis & Visualization

Projet de **Data Analysis et Data Visualization** réalisé dans le cadre de la **Cohorte 2 — Data Science de l'Akieni Academy**.

L'objectif du projet est d'analyser le catalogue **McDonald's Menu 2026** afin de comprendre sa structure, d'évaluer la qualité des données, d'étudier les prix et les caractéristiques nutritionnelles, puis d'identifier les principales relations entre ces variables à travers une démarche d'analyse exploratoire structurée.

---

## 1. Contexte

L'équipe Data Analytics dispose d'un dataset portant sur le **menu McDonald's 2026**.

La mission consiste à :

* comprendre la structure du catalogue ;
* auditer la qualité des données avant toute interprétation ;
* nettoyer et documenter les traitements nécessaires ;
* analyser les prix, les calories et les caractéristiques nutritionnelles ;
* étudier les relations entre les principales variables ;
* identifier les observations atypiques ;
* construire des visualisations pertinentes ;
* sélectionner quelques KPI permettant de synthétiser les résultats ;
* formuler des conclusions cohérentes avec ce que les données permettent réellement d'affirmer.

La démarche suivie est :

> **Comprendre → Auditer → Nettoyer → Valider → Analyser → Visualiser → Interpréter → Synthétiser**

---

## 2. Problématique

> **Que nous apprennent les données du menu McDonald's 2026 sur la relation entre le prix, les calories et les caractéristiques nutritionnelles des produits ?**

L'analyse reste descriptive : le dataset constitue un **catalogue de produits** et non une base de données transactionnelle.

Les résultats ne permettent donc pas de conclure sur les ventes, la rentabilité, la popularité ou la performance commerciale des produits.

---

## 3. Objectifs

Le projet vise à :

* comprendre la structure et le contenu du dataset ;
* évaluer la qualité des données ;
* identifier les valeurs manquantes, doublons, incohérences et valeurs atypiques ;
* vérifier l'unicité des identifiants ;
* analyser la composition du catalogue par catégorie ;
* étudier la distribution des prix ;
* analyser la distribution des calories ;
* étudier les principales variables nutritionnelles ;
* comparer les caractéristiques des produits entre catégories ;
* analyser les relations entre prix, calories et nutrition ;
* étudier les corrélations entre variables numériques ;
* identifier et documenter les observations atypiques ;
* créer des variables dérivées lorsque cela est analytiquement justifié ;
* construire des visualisations répondant à des questions précises ;
* sélectionner des KPI synthétiques ;
* formuler une synthèse et identifier les limites de l'analyse.

---

## 4. Questions analytiques

| Axe               | Question                                                                                    |
| ----------------- | ------------------------------------------------------------------------------------------- |
| **Compréhension** | Combien de produits et de catégories composent le catalogue ?                               |
| **Qualité**       | Les données sont-elles suffisamment cohérentes et exploitables ?                            |
| **Nettoyage**     | Quels traitements sont nécessaires et comment les justifier ?                               |
| **Prix**          | Comment les prix sont-ils distribués et quelles différences observe-t-on entre catégories ? |
| **Calories**      | Comment les calories sont-elles distribuées entre les produits et les catégories ?          |
| **Nutrition**     | Comment les principales variables nutritionnelles se répartissent-elles ?                   |
| **Relations**     | Existe-t-il des associations entre prix, calories et variables nutritionnelles ?            |
| **Corrélations**  | Quelles variables présentent les associations les plus fortes ?                             |
| **Atypiques**     | Quels produits présentent des valeurs éloignées du comportement général ?                   |
| **Visualisation** | Quels graphiques permettent de répondre clairement aux questions analytiques ?              |
| **KPI**           | Quels indicateurs permettent de synthétiser les principaux résultats ?                      |
| **Limites**       | Jusqu'où les données permettent-elles réellement d'interpréter les résultats ?              |

---

## 5. Périmètre des données

Le dataset contient :

* **80 produits** ;
* **9 catégories** ;
* des informations relatives aux produits, aux prix, aux calories et à différentes caractéristiques nutritionnelles.

La granularité du dataset est :

> **1 ligne = 1 produit**

Le fichier CSV fourni constitue la **source de vérité** pour les noms, valeurs et types des variables.

Les conclusions sont donc limitées au périmètre de ce dataset.

---

## 6. Démarche analytique

L'analyse suit une démarche progressive :

```text
Données brutes
      ↓
Data Understanding
      ↓
Data Quality Audit
      ↓
Investigation des anomalies
      ↓
Data Cleaning & Decision
      ↓
Validation
      ↓
Feature Engineering
      ↓
EDA univariée
      ↓
EDA bivariée
      ↓
Corrélations
      ↓
Analyse des valeurs atypiques
      ↓
Data Visualization
      ↓
KPI
      ↓
Synthèse
      ↓
Limites
      ↓
Conclusion
```

Une observation atypique n'est pas automatiquement considérée comme une erreur.

Les décisions de nettoyage sont prises à partir des résultats de l'audit et sont documentées afin de garantir la traçabilité des traitements.

---

## 7. Data Quality Audit

L'audit qualité porte notamment sur :

* les dimensions du dataset ;
* les types de données ;
* les valeurs manquantes ;
* les doublons exacts ;
* l'unicité de `item_id` ;
* les valeurs négatives ;
* les valeurs nulles ;
* les chaînes vides ;
* les variables booléennes ;
* les structures semi-structurées `price_history` ;
* les variables dérivées déjà présentes dans la source ;
* certaines règles de cohérence nutritionnelle.

Des contrôles sont notamment réalisés sur les contraintes suivantes :

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

Certaines relations nutritionnelles sont également contrôlées :

```text
saturated_fat_g <= total_fat_g
trans_fat_g <= total_fat_g
sugars_g <= total_carbs_g
```

Un contrôle spécifique est également réalisé sur la structure et la cohérence de `price_history`.

---

## 8. Nettoyage des données

Les données originales sont conservées dans :

```python
df_raw
```

Les données nettoyées sont stockées dans :

```python
df_clean
```

Puis la table utilisée pour l'analyse est :

```python
df_analysis
```

### Traitement des valeurs négatives nutritionnelles

L'audit a identifié des valeurs négatives dans quatre variables nutritionnelles :

```text
saturated_fat_g
trans_fat_g
dietary_fiber_g
sugars_g
```

Ces valeurs présentent une faible amplitude et sont incohérentes avec la nature des mesures concernées.

La règle de nettoyage retenue consiste à remplacer ces valeurs négatives par leur valeur absolue.

Afin de garantir la traçabilité :

* les données originales restent disponibles dans `df_raw` ;
* un indicateur global `is_changed_value_absolute` identifie les produits concernés ;
* des flags spécifiques permettent d'identifier la variable modifiée.

Cette correction est une **règle de nettoyage documentée** et ne constitue pas une modification de la source brute.

Les valeurs manquantes réellement présentes dans la source sont conservées comme `NaN` et ne sont pas remplacées arbitrairement par zéro, une moyenne ou une médiane.

---

## 9. Feature Engineering

Les variables dérivées sont créées uniquement lorsqu'elles répondent à une question analytique.

Les principaux indicateurs créés sont :

### `price_per_1000_kcal`

Rapporte le prix à 1 000 kcal :

```text
price_usd / calories × 1000
```

### `calories_per_dollar`

Rapporte le nombre de calories au prix :

```text
calories / price_usd
```

### `protein_per_dollar`

Rapporte la quantité de protéines au prix :

```text
protein_g / price_usd
```

### `price_category`

Segmentation descriptive des prix à partir des quartiles de l'échantillon :

```text
Q1
Q2
Q3
Q4
```

Ces indicateurs sont utilisés à des fins **descriptives et comparatives**.

Ils ne constituent pas des mesures de rentabilité ou de « meilleur rapport qualité-prix ».

---

## 10. EDA — Analyse univariée

L'analyse univariée porte notamment sur :

* la répartition des produits par catégorie ;
* les prix ;
* les calories ;
* les variables nutritionnelles ;
* les valeurs minimales et maximales ;
* la moyenne ;
* la médiane ;
* les quartiles ;
* la dispersion des variables.

### Principaux résultats sur les prix

```text
Minimum : 1,19 USD
Maximum : 7,70 USD
Moyenne : 4,08 USD
Médiane : 3,98 USD
Q1      : 2,62 USD
Q3      : 5,32 USD
```

Les prix sont donc compris entre **1,19 USD et 7,70 USD** dans le dataset étudié.

Les prix sont également comparés entre catégories afin d'identifier les différences de niveau et de dispersion.

---

## 11. EDA — Analyse bivariée

L'analyse bivariée étudie principalement :

* **Prix × Calories**
* **Prix × Protéines**
* **Calories × Variables nutritionnelles**

Les relations sont étudiées à l'aide de coefficients de corrélation de **Pearson** et de **Spearman**, complétés lorsque nécessaire par des représentations graphiques telles que les scatterplots.

### Prix × Calories

```text
Pearson  : ≈ 0,41
Spearman : ≈ 0,44
```

L'association est positive et modérée : dans cet échantillon, les produits plus chers ont tendance à être plus caloriques.

### Prix × Protéines

```text
Pearson  : ≈ 0,59
Spearman : ≈ 0,63
```

Cette association est plus forte que celle observée entre prix et calories.

### Calories × Nutrition

Les associations les plus importantes sont observées notamment avec :

```text
Calories × Lipides totaux       ≈ 0,90
Calories × Lipides saturés      ≈ 0,88
Calories × Lipides trans        ≈ 0,78
Calories × Protéines            ≈ 0,75
Calories × Sodium               ≈ 0,72
Calories × Glucides             ≈ 0,72
```

Ces résultats doivent rester descriptifs et ne permettent pas d'établir une causalité.

---

## 12. Analyse des corrélations

Une matrice de corrélation est construite à partir des principales variables numériques analytiques.

Les résultats mettent notamment en évidence :

* une très forte corrélation entre `total_fat_g` et `saturated_fat_g` : **≈ 0,98** ;
* une forte corrélation entre `total_fat_g` et `sodium_mg` : **≈ 0,86** ;
* une forte corrélation entre `total_carbs_g` et `dietary_fiber_g` : **≈ 0,86** ;
* une forte corrélation entre `total_carbs_g` et `sugars_g` : **≈ 0,84**.

Certaines variables présentent au contraire des corrélations faibles ou proches de zéro.

Une corrélation proche de zéro signifie qu'aucune association **linéaire importante** n'est observée dans cet échantillon ; elle ne signifie pas nécessairement qu'il n'existe aucune relation possible.

> **Corrélation ≠ causalité.**

---

## 13. Analyse des valeurs atypiques

Les valeurs atypiques sont étudiées afin de distinguer :

* une éventuelle anomalie de données ;
* une observation réellement extrême mais cohérente avec le catalogue.

Les observations atypiques ne sont donc pas automatiquement supprimées.

Cette approche permet de préserver l'information tout en signalant les observations nécessitant une interprétation prudente.

---

## 14. Data Visualization

Les principales visualisations utilisées sont :

### Composition du catalogue

* Barplot du nombre de produits par catégorie.

### Distribution des prix

* Histogramme des prix.

### Comparaison des catégories

* Boxplot des prix par catégorie.
* Boxplot des calories par catégorie.

### Relations entre variables

* Scatterplot Prix × Calories.
* Scatterplot avec tendance et coefficients de corrélation.

### Corrélations

* Heatmap des corrélations entre variables numériques.

### Synthèse

* Comparaison du prix médian par catégorie.

Chaque visualisation est utilisée pour répondre à une question analytique précise.

---

## 15. KPI

Les principaux KPI retenus sont :

| KPI                         | Valeur / objectif                 |
| --------------------------- | --------------------------------- |
| Nombre total de produits    | 80                                |
| Nombre de catégories        | 9                                 |
| Prix médian                 | 3,98 USD                          |
| Calories médianes           | Indicateur de position centrale   |
| Produit le plus calorique   | Identification du produit extrême |
| Corrélation Prix × Calories | ≈ 0,41                            |
| Top produits caloriques     | Analyse complémentaire            |

Les KPI sont volontairement limités afin de conserver une synthèse lisible et pertinente.

---

## 16. Principaux résultats

L'analyse met en évidence plusieurs constats :

### Structure du catalogue

Le dataset contient **80 produits répartis dans 9 catégories**.

Les catégories ne sont pas représentées de manière uniforme : certaines contiennent davantage de produits que d'autres.

### Prix

Les prix vont de **1,19 USD à 7,70 USD**, avec une moyenne de **4,08 USD** et une médiane de **3,98 USD**.

Des différences de niveaux de prix sont observées entre les catégories.

### Nutrition

Les profils nutritionnels varient fortement selon les familles de produits.

Certaines catégories présentent notamment des niveaux plus élevés de lipides, sodium, glucides ou protéines.

### Relations

Le prix présente une association positive modérée avec les calories et une association plus forte avec les protéines.

Les variables nutritionnelles présentent plusieurs corrélations fortes entre elles, notamment les lipides, glucides, protéines et sodium.

### Qualité des données

Les anomalies identifiées ont fait l'objet d'un audit et de traitements documentés, sans suppression automatique des observations atypiques.

---

## 17. Limites de l'analyse

Les principales limites sont :

### Dataset catalogue

Le dataset ne contient pas de données transactionnelles.

Il ne permet donc pas de mesurer :

* les ventes ;
* les quantités vendues ;
* le chiffre d'affaires ;
* la marge ;
* la rentabilité ;
* la popularité des produits.

### Prix

Les prix analysés sont ceux présents dans le dataset et ne doivent pas être considérés comme des prix universels de McDonald's.

### Taille de l'échantillon

L'analyse porte sur **80 produits et 9 catégories**.

Les résultats doivent donc être interprétés dans le périmètre de cet échantillon.

### Nutrition

Les variables nutritionnelles sont utilisées à des fins descriptives.

Elles ne constituent pas une base suffisante pour produire des recommandations médicales ou nutritionnelles personnalisées.

### Corrélations

Les corrélations indiquent des associations statistiques et ne permettent pas de conclure à une causalité.

### Indicateurs dérivés

Les ratios créés dans le cadre du feature engineering sont descriptifs et ne représentent pas des indicateurs de rentabilité ou de valeur commerciale.

---

## 18. Conclusion

Cette analyse exploratoire a permis de caractériser le catalogue McDonald's Menu 2026 sous plusieurs dimensions : **structure, catégories, prix, calories et caractéristiques nutritionnelles**.

Le projet a d'abord accordé une importance particulière à la qualité des données à travers un audit structuré, puis à un nettoyage documenté et traçable.

L'EDA a ensuite permis d'identifier les principales différences entre catégories et plusieurs associations statistiques importantes entre les variables.

Les résultats montrent notamment une association positive entre le prix et les calories, ainsi que des corrélations fortes entre plusieurs caractéristiques nutritionnelles.

Cependant, ces résultats doivent être interprétés dans le cadre du dataset étudié : il s'agit d'un **catalogue de produits et non d'une base transactionnelle**.

L'analyse permet donc de mieux comprendre la structure et les caractéristiques du menu, mais ne permet pas de conclure sur les ventes, la rentabilité ou la causalité entre les variables.

---

## 19. Reproductibilité

Pour reproduire l'analyse :

### Installation des dépendances

```bash
pip install -r requirements.txt
```

### Lancement de Jupyter

```bash
jupyter notebook
```

Puis ouvrir :

```text
notebooks/mcdonalds_menu_2026_data_analysis.ipynb
```

Le notebook doit être exécuté de manière séquentielle afin de reproduire les différentes étapes de l'analyse.

---

## 20. Structure du repository

```text
mcdonalds-menu-2026-data-analysis/
│
├── data/
│   └── mcdonalds_menu_csv.csv
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

## 21. Technologies utilisées

* **Python 3**
* **Pandas**
* **NumPy**
* **Matplotlib**
* **Seaborn**
* **Jupyter Notebook**
* **Git**
* **GitHub**

---

## 22. Objectif pédagogique

Ce projet constitue une mise en pratique du parcours **Data Science — Cohorte 2 de l'Akieni Academy**.

Il met l'accent sur :

* la qualité des données ;
* le raisonnement analytique ;
* la reproductibilité ;
* la traçabilité des traitements ;
* l'EDA ;
* la visualisation ;
* l'interprétation statistique ;
* la communication des résultats.

L'objectif n'est pas uniquement de produire du code ou des graphiques, mais de construire une **analyse cohérente, justifiée et défendable à l'oral**.

---

## 23. Statut

**Projet finalisé — EDA & Data Visualization**

Le notebook, le nettoyage, l'analyse exploratoire, les corrélations, les visualisations, les KPI, les limites et la conclusion ont été finalisés.

Le projet est prêt pour la **présentation et la soutenance**.

---

## Auteur

**Trésor KITWANDA**

**Akieni Academy — Cohorte 2 Data Science**

Projet Freestyle — EDA & Data Visualization
