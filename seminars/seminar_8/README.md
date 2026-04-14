# Seminar — Building Segmentation using High-Resolution Satellite Imagery

## Overview
This seminar focuses on **binary semantic segmentation** of buildings from high-resolution WorldView satellite imagery. Participants work with large RGB GeoTIFF scenes (0.57 m/pixel) from two study areas — Ventura and Santa Rosa — and corresponding ground-truth building masks.  

The main challenge addressed is the typical size of satellite images (thousands of pixels in width and height). The seminar teaches how to split large rasters into smaller patches (e.g. 512×512), train modern CNN architectures, apply data augmentations, and merge predictions back into a full-resolution building mask map.

---

## Objectives
- Understand the specifics of semantic segmentation on high-resolution remote sensing data  
- Learn to handle large GeoTIFF images by creating manageable patches  
- Train and evaluate CNN models for building footprint extraction  
- Apply data augmentations to improve model generalization  
- Merge patch-level predictions into a seamless full-scene mask  
- Experiment with different segmentation architectures using `segmentation_models.pytorch`  
- Visualize and quantitatively assess segmentation results  

---

## Structure

```
building_segmentation/
│
├── Building_segmentation_seminar.ipynb   ← main notebook with full pipeline
├── building_segmentation/
│   ├── ventura/                          ← RGB .tif files + all.tif (labels)
│   └── santa_rosa/                       ← RGB .tif files + all.tif (labels)
│
└── README.md
```

- **Building_segmentation_seminar.ipynb** — complete workflow (data preparation, patching, training, evaluation, visualization)  
- **data/** — high-resolution WorldView RGB imagery and binary building masks for two sites  

---

## Setup

### Install dependencies
```bash
pip install torch torchvision torchaudio rasterio matplotlib albumentations segmentation-models-pytorch scikit-learn
```

> Note: Use GPU if available (`device = "cuda"`).

---

## Data Description

The dataset consists of two study sites (Ventura and Santa Rosa). All images are georeferenced GeoTIFF files.

| File              | Description                                      | Resolution | Channels |
|-------------------|--------------------------------------------------|------------|----------|
| `*.tif` (R,G,B)     | High-resolution WorldView satellite imagery      | 0.57 m/pixel | 1 (for each RGB channel separately) |
| `all.tif`         | Binary building mask (ground truth)              | 0.57 m/pixel | 1       |

- **Task**: Binary semantic segmentation (building vs. background)  
- Images are very large → the notebook demonstrates cropping into 512×512 (or custom size) patches for training.

---

## Workflow

1. Load RGB imagery and corresponding binary masks using `rasterio`  
2. Create fixed-size patches (e.g. 512×512) from large scenes  
3. Build a custom PyTorch `Dataset` for patch-based training  
4. Apply data augmentations (Albumentations) to increase dataset diversity  
5. Prepare your self-created U-Net model 
6. Train a segmentation model (baseline: U-Net; advanced: architectures from `segmentation_models.pytorch`)  
7. Evaluate using IoU, Dice coefficient, Precision, Recall, F1-score  
8. Generate predictions on the chosen test area  
9. Merge patch predictions back into a full-resolution binary mask  
10. Visualize original image, ground truth, and predicted mask side-by-side  

---

## Key Concepts

### Semantic Segmentation in Remote Sensing
Predicting a class for **every pixel** in an image. Here: buildings (1) vs. non-buildings (0).

### Patching Strategy
Satellite images are too large for direct GPU processing. The solution is to:
- Split the original scene into overlapping or non-overlapping patches
- Train on patches
- Stitch predictions back together (with optional blending on overlaps)

### Modern Segmentation Tools
- **Albumentations** — fast and powerful image augmentations tailored for segmentation  
- **segmentation_models.pytorch** — ready-to-use U-Net, DeepLabV3+, PSPNet, LinkNet, etc. with dozens of encoders (ResNet, EfficientNet, MobileNet, etc.)

---

## Outcome
- Ability to perform end-to-end semantic segmentation on real high-resolution satellite imagery  
- Practical experience handling large geospatial rasters through patching  
- Skills in data augmentation and modern segmentation libraries  
- Understanding of evaluation metrics specific to segmentation tasks  
- Confidence to experiment with different CNN architectures for remote sensing problems  

---

## Resources
- [segmentation_models.pytorch documentation](https://github.com/qubvel-org/segmentation_models.pytorch)  
- [Albumentations documentation](https://albumentations.ai/docs/)  
- Rasterio Docs: https://rasterio.readthedocs.io  
- U-Net paper: https://arxiv.org/abs/1505.04597  
- WorldView satellite imagery characteristics  

---

