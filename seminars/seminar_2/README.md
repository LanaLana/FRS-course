# Seminar 2 — Multispectral Data and Index Calculation

## Overview
This seminar focuses on working with **multispectral satellite data** in QGIS.  
It covers how to combine spectral bands, calculate remote sensing indexes, and create raster and vector masks for analyzing natural phenomena.

---

## Objectives
- Understand multispectral imagery and band structure  
- Create multiband raster images  
- Calculate indexes (NDVI, NDWI, NBR, etc.)  
- Use raster calculator for analysis  
- Create binary raster masks  
- Create vector layers (shapefiles)  

---

## Structure
```
seminar_2/
│
├── presentation/
│ └── QGIS_multispectral.pdf
│
└── README.md
```

- **presentation/** — theory + QGIS operations demo (multispectral data, indexes, masks)  
- **README.md** — instructions  

---

## Setup
Install QGIS:  
https://qgis.org/resources/installation-guide/

---

## Data Source
Use **Sentinel Hub EO Browser**:  
https://apps.sentinel-hub.com/eo-browser  

- Register  
- Search Sentinel-2 imagery  
- Download raw bands (GeoTIFF)  

---

## Workflow
1. Download Sentinel-2 bands for selected area  
2. Load bands into QGIS  
3. Create multiband image (Virtual Raster)  
4. Visualize bands (e.g., RGB: 3, 2, 1)  
5. Calculate indexes using raster calculator  
6. Create raster mask using threshold  
7. Create vector layer (shapefile)  
8. Digitize objects (polygons)  

---

## Example Analysis (Indexes)
Common indexes (check seminar slides):
```
NDVI = (B8 - B4) / (B8 + B4)
NDWI = (B03 - B08) / (B03 + B08)
Moisture Index = (B9 - B11) / (B9 + B11)
NBR = (B8 - B12) / (B8 + B12)
```


---

## How to?

### Multiband Image and Indexes creation
1. Create multiband raster:
   - Raster → Miscellaneous → Build Virtual Raster  
   - Add bands as separate layers  
   - Set resolution  

2. Visualize:
   - Set RGB combination (3, 2, 1)  

3. Calculate indexes:
   - Raster → Raster Calculator  
   - Write expression  
   - Save result  

---

### Create Raster Binary Mask

Steps:
1. Define threshold for index  
2. Apply raster calculator to mask image with selected threshold
 

---

### Create Vector Mask (Shapefile)
Create vector layer and digitize objects.

Steps:
1. Layer → Create Layer → New Shapefile Layer  
2. Choose geometry type (Polygon)  
3. Enable editing  
4. Draw polygons  

---

## Final Task
Find a Sentinel-2 image of a natural disaster and:

1. Create multiband image  
2. Calculate index  
3. Generate raster mask  
4. Create vector mask  

Examples:
- Oil spill  
- Floods  
- Fires  

---

## Outcome
- Multiband raster visualization  
- Calculated index (e.g., NDVI, NDWI)  
- Binary raster mask  
- Vector shapefile with selected objects  

---

## Resources
- QGIS Docs: https://docs.qgis.org  
- Sentinel Hub: https://docs.sentinel-hub.com  
- Sentinel-2 bands: https://gisgeography.com/sentinel-2-bands-combinations/  