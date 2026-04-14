# Seminar 6 — ML Regression for Forest Growing Stock Volume Estimation

## Overview
This seminar demonstrates how machine learning regression can be applied to real-world remote sensing data to estimate **Growing Stock Volume (GSV)** — the total over-bark volume of living trees in a forest area, measured in m³/ha.

The study area is Perm Krai, Russia. Ground-based inventory measurements from 2020 are combined with **Sentinel-2** multispectral imagery and auxiliary raster layers (canopy height, elevation, forest age) to build a predictive model.

The seminar covers the full pipeline: from raw raster data processing and feature engineering at the plot level, to training and evaluating ensemble regression models.

> **Supplementary material:** `Random_Forests_seminar.ipynb` provides a standalone introduction to decision trees and random forests — read it first if you are unfamiliar with these algorithms.

---

## Objectives
- Understand the task of forest attribute estimation from satellite data
- Load and visualize multispectral raster data (GeoTIFF)
- Merge multiple raster layers into a single feature stack
- Work with vector data using GeoPandas (points → buffered polygons)
- Extract per-plot statistics from raster data
- Calculate spectral indices (NDVI, EVI)
- Train and compare regression models: Decision Tree, Random Forest, XGBoost
- Evaluate models with MAPE and MAE
- Apply K-Fold cross-validation

---

## Structure

```
seminar_6/
│
├── GSV_preprocessing.ipynb            ← main notebook
├── Random_Forests_seminar.ipynb       ← supplementary: RF theory and examples
│
├── timberstock/
│   ├── 2022.tif     — Sentinel-2 composite (10 spectral bands, 10 m resolution)
│   ├── 2023.tif     — Sentinel-2 composite for 2023
│   ├── chm.tif      — Canopy Height Model
│   ├── dem.tif      — Digital Elevation Model
│   ├── age.tif      — Forest age (estimated by ML)
│   └── data.csv     — Field inventory: plot coordinates + timber volume (V)
│
└── README.md
```
- **GSV_preprocessing.ipynb** — full ML pipeline for GSV estimation
- **Random_Forests_seminar.ipynb** — RF theory and examples (supplementary)
- **timberstock/** — GSV dataset (downloaded using wget)
- **README.md** — instructions
---

## Setup

### Install dependencies
```bash
pip install numpy pandas matplotlib rasterio geopandas tifffile folium mapclassify shapely seaborn scikit-learn xgboost
```

### Download data
The dataset is downloaded directly in the notebook from a shared link:
```bash
wget https://getfile.dokpub.com/yandex/get/https://disk.yandex.ru/d/yqVOed67gKPefg -O ./GSV_dataset.zip
unzip ./GSV_dataset.zip
```

---

## Data Description

### Raster layers
All layers share the same spatial extent and 10 m/pixel resolution:

| File | Description |
|---|---|
| `2022.tif` | Sentinel-2 composite — 10 spectral bands: B02, B03, B04, B05, B06, B07, B08, B8A, B11, B12 |
| `chm.tif` | Canopy Height Model — tree height in meters |
| `dem.tif` | Digital Elevation Model — terrain elevation |
| `age.tif` | Forest age estimated by a separate ML model |

### Field inventory (`data.csv`)
Each record is a circular plot with radius 9 m:

| Column | Description |
|---|---|
| `x`, `y` | Plot coordinates (EPSG:32640) |
| `V` | Target variable: timber volume in m³/ha |

---

## Workflow

### 1. Load and visualize raster data
- Open GeoTIFF files with `rasterio`
- Inspect metadata (CRS, resolution, band count, nodata)
- Visualize individual bands and auxiliary layers (DEM, CHM, forest age)

### 2. Merge raster layers
- Concatenate all 13 bands (10 spectral + CHM + DEM + AGE) into a single feature raster
- Save merged raster to `merged_data.tif`

### 3. Prepare vector data
- Load inventory CSV with `pandas`
- Convert plot coordinates to `Point` geometries using `shapely`
- Create a `GeoDataFrame` with `geopandas`
- Apply 9 m buffer to convert points to circular polygons
- Visualize plots on an interactive map

### 4. Extract per-plot features
For each inventory plot, crop the merged raster and compute **5 statistics per band**:
`min`, `max`, `mean`, `median`, `std`

This yields **65 features** (13 bands × 5 statistics) + coordinates.

> **Why statistics and not raw pixels?**
> The target (GSV) is defined at the plot level. Aggregating pixel values into statistics aligns the scale of predictors and response, and reduces sensitivity to geolocation errors.

### 5. Calculate spectral indices
Add NDVI and EVI for each statistic:
```
NDVI = (B08 - B04) / (B08 + B04)
EVI  = 2.5 * (B08 - B04) / (B08 + 6*B04 - 7.5*B02 + 1)
```

### 6. Explore the data
- Plot histogram and KDE of the target variable (V)
- Compute correlation matrix across features

### 7. Train and evaluate models
Split data 2/3 train, 1/3 test (random shuffle). Train and compare:

| Model | Notes |
|---|---|
| Decision Tree | Shallow tree (max_depth=3) as interpretable baseline |
| Random Forest | 200 trees, no scaling needed |
| XGBoost | 800 estimators, MinMax scaling applied |

Metrics: **MAPE** and **MAE**

### 8. Cross-validation
Apply 5-fold cross-validation with `KFold` for a more robust performance estimate.

---

## Key Concepts

### Growing Stock Volume (GSV)
Total over-bark volume of all living trees in a forest area (m³/ha). Estimated from ground measurements and predicted from satellite imagery using ML.

### Feature Engineering at Plot Level
Rather than working pixel-by-pixel, we extract per-plot summary statistics from raster data. This is appropriate when the target is measured at the plot level and plot size is comparable to or larger than pixel resolution.

### Ensemble Regression
Random Forest and XGBoost are ensemble methods — they combine many weak learners (decision trees) to produce a stronger, more generalizable model.

---

## Outcome
- Experience building an end-to-end ML pipeline on real geospatial data
- Ability to merge and process multi-source raster data
- Hands-on practice with raster-vector integration for feature extraction
- Understanding of plot-level feature aggregation
- Ability to train and compare regression models
- Understanding of cross-validation for small datasets

---

## Resources
- Rasterio Docs: https://rasterio.readthedocs.io
- GeoPandas Docs: https://geopandas.org
- Scikit-learn Ensemble Methods: https://scikit-learn.org/stable/modules/ensemble.html
- XGBoost Docs: https://xgboost.readthedocs.io
- Sentinel-2 bands: https://gisgeography.com/sentinel-2-bands-combinations/
