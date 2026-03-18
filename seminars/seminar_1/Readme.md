# Seminar 1 — Introduction to QGIS

## Overview
This seminar introduces the basics of **QGIS** and working with satellite imagery.  
It is designed so a new employee can independently explore core workflows used in geospatial analysis.

---

## Objectives
- Understand QGIS basics  
- Load and visualize spatial data  
- Work with Sentinel-2 imagery  
- Use basic tools (measurement, raster calculator)  
- Perform simple analysis (e.g., NDVI)  

---

## Structure
```
seminar_1/
│
├── presentation/
│ └── QGIS_intro.pdf
│
├── Norilsk_oil_spill/
│ ├── *.tiff (example satellite images)
│
└── README.md
```


- **presentation/** — theory + demo (QGIS basics, tools, Sentinel, NDVI)  
- **Norilsk_oil_spill/** — sample data for practice  
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
- Download GeoTIFF  

---

## Workflow
1. Load `.tiff` into QGIS (drag & drop)  
2. Adjust CRS if needed  
3. Explore layer properties  
4. Add basemap (optional)  
5. Use tools: measure, identify, raster calculator  

---

## Example Analysis (NDVI)
```NDVI = (NIR - Red) / (NIR + Red)```


---

## Task
Find a Sentinel-2 image of a **natural disaster** and visualize it in QGIS.

Examples:
- Oil spill  
- Floods  
- Fires  

Steps:
1. Download data  
2. Load into QGIS  
3. Visualize  
4. (Optional) run NDVI  

---

## Outcome
- Map or exported image  
- Basic visualization  
- (Optional) simple analysis  

---

## Resources
- QGIS Docs: https://docs.qgis.org  
- Sentinel Hub: https://docs.sentinel-hub.com  
