# Seminar 7 — ML Classification for Oil Spill Detection

## Overview
This seminar demonstrates how machine learning classification can be applied to satellite imagery for detecting oil spills.

The study area is **Norilsk, Russia**, where a major diesel fuel spill occurred in May–June 2020. Using **Sentinel-2** multispectral imagery from three dates around the event, the task is a **binary classification problem**: determine whether a given pixel belongs to an oil-contaminated area or not.

The seminar covers the full pipeline: from preparing a labeled dataset using a vector mask, handling class imbalance with SMOTE, to training and evaluating multiple classification models.

---

## Objectives
- Understand the remote sensing context of oil spill detection
- Load and inspect multispectral raster data with rasterio
- Use a vector mask (GeoJSON) to label pixels as oil / non-oil
- Construct a pixel-level tabular dataset from raster data
- Handle severe class imbalance using SMOTE
- Train and compare multiple classification models
- Evaluate models with accuracy, F1-score, confusion matrix, and ROC-AUC

---

## Structure

```
seminar_7/
│
├── seminar_7.ipynb                  ← main notebook
│
├── data/
│   └── Norilsk_oil_spill/
│       ├── 01-06-2020.tiff          — Sentinel-2 image after spill
│       ├── 23-05-2020.tiff          — Sentinel-2 image before spill
│       └── 31-05-2020.tiff          — Sentinel-2 image during spill (used for training)
│
├── oil_mask_01062020.geojson        — vector mask of oil-contaminated area (June 1)
├── oil_mask_31052020.geojson        — vector mask of oil-contaminated area (May 31)
│
└── README.md
```

---

## Setup

### Install dependencies
```bash
pip install numpy pandas matplotlib rasterio geopandas scikit-learn imbalanced-learn seaborn
```

---

## Data Description

### Raster imagery
Three Sentinel-2 scenes of the Norilsk area at different dates. Each scene contains **14 bands**:

| Bands | Description |
|---|---|
| B01–B09, B11, B12 | Spectral bands (visible, NIR, SWIR) |
| SCL | Scene Classification Layer |
| CLM | Cloud Mask |

### Vector masks (GeoJSON)
Manually digitized polygons marking oil-contaminated pixels on the surface. Used as ground truth labels for supervised learning.

---

## Workflow

### 1. Prepare the labeled mask
- Load the oil spill vector mask from GeoJSON using `geopandas`
- Open the corresponding Sentinel-2 scene with `rasterio`
- Apply `rasterio.mask.mask()` to extract pixels inside the oil polygon
- Build a binary class layer:
  - `1` — non-oil pixels
  - `2` — oil pixels
  - `NaN` — outside the area of interest

### 2. Build a pixel-level dataset
- Concatenate all 14 spectral bands with the class label into a single array of shape `(15, H, W)`
- Reshape to a 2D table: each row is one pixel, each column is a band or the label
- Drop rows with NaN values
- Result: a DataFrame with columns `B01`–`B12`, `SCL`, `CLM`, `isOil`

### 3. Preprocess features
- Scale features using `StandardScaler`
- Apply **SMOTE** to oversample the minority class (oil pixels) and balance the dataset

### 4. Split data
- 67% training / 33% test split after SMOTE

### 5. Train and evaluate models
Train three classifiers and compare results using a shared `report()` function that prints accuracy, classification report, confusion matrix, and ROC-AUC curve:

| Model | Notes |
|---|---|
| AdaBoost | 100 estimators, boosting ensemble |
| Decision Tree | max_depth=5, interpretable baseline |
| Random Forest | max_depth=2, bagging ensemble |
| SVM | Available in code but commented out (computationally heavy) |

---

## Key Concepts

### Pixel-level classification
Unlike the plot-level regression in Seminar 6, here each pixel is treated as an independent sample. This is appropriate when the target is defined at the pixel level and high spatial resolution is available.

### Class imbalance
Oil spill pixels are rare compared to the total scene area. Training directly on imbalanced data leads to high overall accuracy but poor detection of the minority class (oil). **SMOTE** synthesizes new minority-class samples to address this.

### Evaluation metrics
- **Confusion matrix** — shows true/false positives and negatives
- **Classification report** — precision, recall, F1-score per class
- **ROC-AUC** — model performance across all decision thresholds; AUC closer to 1.0 indicates better class separation

---

## Outcome
- Experience building a pixel-level classification pipeline from satellite data
- Ability to use vector masks to generate labeled datasets from raster imagery
- Understanding of class imbalance and how to address it with SMOTE
- Hands-on practice with ensemble classifiers (AdaBoost, Random Forest)
- Ability to interpret confusion matrices and ROC-AUC curves in an environmental context

---

## Resources
- Rasterio Docs: https://rasterio.readthedocs.io
- GeoPandas Docs: https://geopandas.org
- Scikit-learn Ensemble Methods: https://scikit-learn.org/stable/modules/ensemble.html
- Imbalanced-learn (SMOTE): https://imbalanced-learn.org
- Sentinel-2 bands: https://gisgeography.com/sentinel-2-bands-combinations/
- Norilsk oil spill (2020): https://en.wikipedia.org/wiki/2020_Norilsk_oil_spill
