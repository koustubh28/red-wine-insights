# 🍷 Red Wine Quality — Exploratory Data Analysis
> Exploratory Data Analysis on the UCI Red Wine Quality dataset — uncovering which physicochemical properties of Portuguese Vinho Verde red wines most influence expert quality ratings.

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Dataset](#-dataset)
- [Project Steps](#-project-steps)
- [Key Findings](#-key-findings)
- [Visualisations](#-visualisations)
- [Tech Stack](#-tech-stack)
- [Getting Started](#-getting-started)

---

## 🔍 Overview

This project performs a full Exploratory Data Analysis (EDA) on the well-known Red Wine Quality dataset. The goal is to understand the dataset's structure, clean it, and identify which chemical features have the strongest relationship with wine quality scores assigned by expert tasters.

**Central question:** Which physicochemical properties most strongly predict the quality of red wine?

---

## 📊 Dataset

| Attribute | Detail |
|-----------|--------|
| **Source** | [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/wine+quality) |
| **File** | `winequality-red.csv` (semicolon-separated) |
| **Raw rows** | 1,599 |
| **Rows after cleaning** | 1,359 |
| **Feature columns** | 11 physicochemical inputs |
| **Target column** | `quality` — integer score from 3 to 8 |
| **Missing values** | None |

### Features

| Feature | Description |
|---------|-------------|
| `fixed acidity` | Tartaric acid content |
| `volatile acidity` | Acetic acid — high levels cause vinegary taste |
| `citric acid` | Adds freshness and flavour |
| `residual sugar` | Sugar remaining after fermentation |
| `chlorides` | Salt content |
| `free sulfur dioxide` | Free form of SO₂ — prevents microbial growth |
| `total sulfur dioxide` | Total SO₂ (free + bound) |
| `density` | Density of wine (close to water) |
| `pH` | Acidity/basicity on 0–14 scale |
| `sulphates` | Additive contributing to SO₂ levels |
| `alcohol` | Percentage alcohol by volume |
| `quality` | **Target** — expert rating from 3 (worst) to 8 (best) |

---

## 🔬 Project Steps

### 1. Load & Inspect
- Loaded CSV using `pd.read_csv()` with `sep=';'`
- Inspected shape **(1599 × 12)**, data types, and null counts using `df.info()` and `df.describe()`
- Confirmed **zero missing values** across all 12 columns

### 2. Duplicate Detection & Removal
- Found **240 duplicate rows** using `df.duplicated()`
- Removed with `df.drop_duplicates(inplace=True)`
- Final clean dataset: **1,359 rows × 12 columns**

### 3. Correlation Analysis
- Computed full pairwise Pearson correlation matrix using `df.corr()`
- Visualised with an annotated seaborn heatmap
- Identified top correlates with quality:

| Feature | Correlation with Quality |
|---------|--------------------------|
| `alcohol` | **+0.48** (strongest positive) |
| `volatile acidity` | **-0.40** (strongest negative) |
| `sulphates` | +0.25 |
| `citric acid` | +0.23 |
| `total sulfur dioxide` | -0.18 |
| `density` | -0.18 |

### 4. Visualisations
- **Quality distribution bar chart** — shows class distribution across scores 3–8
- **Alcohol histogram** — distribution of alcohol content across all wines
- **Box plot: alcohol vs quality** — confirms the positive trend between alcohol and quality rating

---

## 💡 Key Findings

- **Alcohol is the #1 predictor of quality** (r = +0.48). Higher alcohol content consistently correlates with higher expert ratings, likely due to the fuller body and warmth it contributes.
- **Volatile acidity hurts quality** (r = -0.40). High acetic acid levels produce a vinegary, unpleasant taste that experts penalise.
- **Sulphates have a moderate positive effect** (r = +0.25), acting as a preservative that keeps the wine fresher.
- **Class imbalance exists** — over 80% of wines score 5 or 6. Wines rated 3 or 8 are rare, which is important to consider for any downstream classification task.
- **Density and pH show weak correlations** with quality (-0.18 and -0.06 respectively), suggesting they are less useful as standalone predictors.

---

## 📈 Visualisations

### Correlation Heatmap
Shows all pairwise feature correlations. Alcohol-quality (+0.48) and volatile acidity-quality (-0.40) stand out clearly.

### Quality Distribution
Most wines score 5 (most common) or 6. Very few score 3 or 8, reflecting the natural scarcity of extremely poor or excellent wines in the sample.

### Alcohol vs Quality (Box Plot)
Box plots per quality level show the median alcohol rising consistently from quality 3 through quality 8 — a clear visual confirmation of the strongest correlation in the dataset.

---

## 🛠 Tech Stack

| Library | Purpose |
|---------|---------|
| `pandas` | Data loading, inspection, cleaning, correlation |
| `matplotlib` | Base plotting |
| `seaborn` | Heatmap, histogram, categorical box plots |

---

## 🚀 Getting Started

### Prerequisites

```bash
pip install pandas matplotlib seaborn jupyter
```

### Run

1. Clone the repository
2. Place `winequality-red.csv` in the project root
3. Open `red_wine.ipynb` in Jupyter Notebook
4. Run all cells top to bottom

---

## 📌 What's Next

- [ ] Build a classification model (Random Forest / Logistic Regression) to predict quality
- [ ] Feature engineering — interaction terms between correlated features

---

## 📄 Data Source
P. Cortez, A. Cerdeira, F. Almeida, T. Matos and J. Reis. Modeling wine preferences by data mining from physicochemical properties. Decision Support Systems, 2009.
Dataset available at the UCI Machine Learning Repository.
P. Cortez, A. Cerdeira, F. Almeida, T. Matos and J. Reis. *Modeling wine preferences by data mining from physicochemical properties.* Decision Support Systems, 2009.
Dataset available at the [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/wine+quality).
