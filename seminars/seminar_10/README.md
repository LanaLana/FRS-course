# Seminar 10 — Reports in QGIS

## Overview
This seminar teaches you how to create professional cartographic reports in QGIS.  
You will work with real vector data (fire probability grids and administrative boundaries) to visualize wildfire risk in the Primorsky region, process layers, build a clean report layout, and export a ready-to-share PDF.

---

## Objectives
- Load and visualize vector GeoJSON data  
- Apply graduated symbology to probability data  
- Process vector layers (split, filter, merge)  
- Create and customize reports using QGIS **Report Layout**  
- Add professional map elements (labels, grids, scale bars, north arrows)  
- Export a complete PDF report  

---

## Structure
```
seminar_10/
│
├── presentation/
│   └── FRS_Course._Seminar_QGIS_report.pdf
│
├── data/
│   ├── fire_probability_01032025.geojson
│   ├── primorskiy_region.geojson
│   ├── baseline_vit_Siberian_FINAL_Nesterov_14_lightning_GFS_Sib_2019-03-31_00_00_00.geojson
│   └── example.pdf
│
└── README.md
```

- **presentation/** — step-by-step seminar slides (with screenshots)  
- **data/** — all input files and example output  
- **README.md** — instructions  

---

## Setup
Install the latest **QGIS** (recommended: version 3.28 or newer):  
https://qgis.org/resources/installation-guide/

No additional plugins are required.

---

## Data Source
All data is provided as GeoJSON vector files:

- `fire_probability_01032025.geojson` — fire probability grid (day_5 column) for the Primorsky region  
- `primorskiy_region.geojson` — administrative districts of Primorsky Krai  
- `baseline_vit_Siberian_FINAL_Nesterov_14_lightning_GFS_Sib_2019-03-31_00_00_00.geojson` — final task fire probability grid for Siberia

---

## Workflow
1. Open QGIS and load all input data  
2. Style the fire probability layer  
3. Process districts (split → select high-probability areas → merge)  
4. Create a new Report project  
5. Build the report layout (labels, map, grid, scale bar, north arrow)  
6. Export as PDF  

---

## How to?

### 1. Open QGIS and visualize input data
- Drag and drop all three GeoJSON files into QGIS  
- Explore the layers in the map canvas

### 2. Visualize fire probability
1. Open **Layer Properties → Symbology** for `fire_probability_01032025.geojson`  
2. Choose **Graduated** renderer  
3. Column: `day_5`  
4. Color ramp: **Reds**  
5. Opacity: 0–80%  
6. Classes: 10  
7. Classification mode: **Natural breaks**  
8. Apply and close

### 3. Visualize districts (high fire probability)
1. Use **Vector → Data Management Tools → Split vector layer** on `primorskiy_region.geojson`  
2. Add the resulting layers to the map  
3. Create a **layer group** named “Districts”  
4. Remove all unaffected (low-probability) districts  
5. Merge the selected high-probability districts  
6. Set layer opacity to **30%**

### 4. Create report
1. Go to **Project → New Report**  
2. Give the report a name (e.g., “Fire_Probability_Primorsky”) and click OK  
3. In the Report Organizer, add a new **Section**  
4. Click the **Edit** button to open the layout editor

### 5. Build the report layout
- **Add label**: Use the label tool (T) → edit text in Item Properties (title: “Fire probability prediction for Primorsky region”)  
- **Add map**: Use the map tool → draw the map area → in Item Properties set CRS and scale (recommended: 1:100000)  
- **Add grid**: In Map Item Properties → Grids → Modify Grid…  
  - Set grid CRS  
  - Define intervals  
  - Adjust line style and labels  
- **Add map elements**:  
  - Scale bar  
  - North arrow  

### 6. Export
1. Go to **Layout → Export Report as PDF**  
2. Adjust export settings if needed  
3. Save your final report

---

## Task
1. Create a visualization of the file  
   `baseline_vit_Siberian_FINAL_Nesterov_14_lightning_GFS_Sib_2019-03-31_00_00_00.geojson`  
2. Create a report project using QGIS.  
3. Customize your report. Add scale bar, grid, labels, legend and North arrow.  
4. Export as PDF.

---

## Outcome
By the end of this seminar you will be able to:
- Produce clean, professional PDF reports directly from QGIS  
- Effectively present geospatial analysis results (e.g. fire risk maps)  
---

## Resources
- QGIS Documentation (Reports & Layouts): https://docs.qgis.org  
- QGIS Report Layout tutorial: https://docs.qgis.org/latest/en/docs/training_manual/map_composer/index.html  
- Seminar slides: `presentation/FRS_Course._Seminar_QGIS_report.pdf` (contains all screenshots and detailed instructions)

---
