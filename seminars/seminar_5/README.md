# Seminar 5 — Exoplanet Detection: Binary Classification with Machine Learning

## Overview
This seminar demonstrates how machine learning can be applied to real NASA Kepler mission data to detect exoplanets.  
Each star in the dataset is characterized by a time series of flux (light intensity) measurements. The task is a **binary classification problem**: determine whether a star has at least one exoplanet in orbit based on the pattern of its light curve.

The seminar covers the full ML pipeline — from exploratory data analysis and signal preprocessing to model training, class imbalance handling, and evaluation.

---

## Objectives
- Understand the physical context of the exoplanet detection problem
- Explore and visualize time series flux data
- Detect and handle class imbalance
- Preprocess signal data (normalization, Gaussian filtering, feature scaling)
- Train and compare multiple classification models
- Evaluate models using classification report, confusion matrix, and ROC-AUC
- Apply SMOTE to balance classes and improve model performance

---

## Structure

```
seminar_5/
│
├── data/
│   ├── exoTrain.csv
│   └── exoTest.csv
├── seminar_5_exoplanet-exploration.ipynb
└── README.md
```

- **notebook** — full ML pipeline from EDA to model evaluation
- **data/** — Kepler K2 mission flux time series dataset
- **README.md** — instructions

---

## Setup

### Install dependencies
```bash
pip install numpy pandas matplotlib scikit-learn seaborn imbalanced-learn scipy
```

---

## Data Description

The dataset contains flux (light intensity) observations from the NASA Kepler K2 mission.

Each record includes:
- `LABEL` — binary target: `2` = star with confirmed exoplanet(s), `1` = star without exoplanet
- `FLUX.1` – `FLUX.3197` — light intensity measurements recorded at ~30-minute intervals

The dataset is highly imbalanced: ~5050 non-exoplanet stars vs. ~37 confirmed exoplanet stars in the training set.

---

## Workflow

1. Load and explore train and test datasets
2. Remap labels to binary values (0 / 1)
3. Visualize flux time series for individual stars
4. Analyze class distribution
5. Check for missing values
6. Plot correlation matrix
7. Visualize flux distributions (Gaussian histograms, box plots)
8. Detect and remove outliers
9. Prepare features and target variables
10. Normalize flux signals (L2 row-wise normalization)
11. Apply Gaussian filter for signal smoothing
12. Apply feature scaling (StandardScaler, fit on train only)
13. Train baseline models: KNN, Logistic Regression, Decision Tree
14. Evaluate models: accuracy, classification report, confusion matrix, ROC-AUC
15. Balance classes using SMOTE
16. Re-train and re-evaluate models on balanced data
17. Compare results before and after class balancing

---

## Key Concepts

### Class Imbalance
The dataset is heavily skewed toward non-exoplanet stars. Training on raw data leads to misleadingly high accuracy while the minority class (exoplanet stars) is poorly detected. This is addressed using **SMOTE**.

### Signal Preprocessing
Each row is a time series signal, so preprocessing follows signal processing logic:
- **L2 row-wise normalization** — removes differences in signal amplitude, preserves shape
- **Gaussian filter** — smooths high-frequency noise while preserving the signal's overall pattern
- **StandardScaler (column-wise)** — standardizes each time step across all samples; fitted on train data only to prevent data leakage

### Evaluation Metrics
- **Confusion matrix** — shows true/false positives and negatives
- **Classification report** — precision, recall, F1-score per class
- **ROC-AUC** — evaluates model performance across all decision thresholds; AUC closer to 1.0 indicates better class separation

---

## Models

| Model | Notes |
|---|---|
| K-Nearest Neighbors (KNN) | Distance-based classifier |
| Logistic Regression | Linear model with class weight adjustment |
| Decision Tree | Tree-based model with depth limit |

All models are trained and evaluated both **before** and **after** SMOTE oversampling.

---

## Outcome

- Experience working with real satellite mission data
- Ability to explore and visualize time series datasets
- Understanding of signal preprocessing for ML
- Hands-on practice with binary classification models
- Ability to recognize and handle class imbalance with SMOTE
- Ability to interpret confusion matrices and ROC-AUC curves

---

## Resources

- Scikit-learn Docs: [https://scikit-learn.org/stable/](https://scikit-learn.org/stable/)
- Imbalanced-learn (SMOTE): [https://imbalanced-learn.org](https://imbalanced-learn.org)
- NASA Kepler Mission: [https://www.nasa.gov/kepler](https://www.nasa.gov/kepler)
- Dataset source (Kaggle): [https://www.kaggle.com/datasets/keplersmachines/kepler-labelled-time-series-data](https://www.kaggle.com/datasets/keplersmachines/kepler-labelled-time-series-data)
