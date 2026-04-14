# Seminar 4 — Rasterio and GeoPandas

## Overview
This seminar introduces working with geospatial data in Python using **rasterio** and **geopandas**.  
It covers reading, processing, and analyzing raster and vector data, as well as combining them in geospatial workflows.

---

## Objectives
- Understand raster data handling with rasterio  
- Read and manipulate raster datasets  
- Work with vector data using geopandas  
- Perform spatial operations  
- Combine raster and vector data  
- Clip data in raster and vector workflows  
- Build raster mosaics from multiple scenes  

---

## Structure
```

seminar_4/
│
├── notebooks/
│ ├── seminar_4_rst.ipynb
│ ├── seminar_4_rst_p2.ipynb
│ └── seminar_4_gpd.ipynb
│
├── data/
│ └── (raster and vector files)
│
└── README.md

```

- **notebooks/** — rasterio and geopandas workflows  
- **data/** — raster and vector datasets  
- **README.md** — instructions  

---

## Setup

### Install dependencies
```bash
pip install rasterio geopandas matplotlib shapely
````

---

## Data Source

* Raster data (GeoTIFF)
* Vector data (Shapefiles / GeoJSON)

---

## Workflow

1. Load raster data using rasterio
2. Inspect raster metadata
3. Read raster bands
4. Load vector data using geopandas
5. Perform spatial operations
6. Combine raster and vector data
7. Clip raster and vector layers
8. Create raster mosaics from several files

---

## Considered Functions

### Rasterio Functions

#### `rasterio.open()`

**Description:** Opens a raster dataset.

* **Input:**

  * File path to raster (e.g., `.tif`)
  * Optional mode (`'r'`, `'w'`)

* **Output:**

  * Dataset object

---

#### `dataset.read()`

**Description:** Reads raster data from dataset.

* **Input:**

  * Band index (optional)

* **Output:**

  * NumPy array of raster values

---

#### `dataset.meta`

**Description:** Returns metadata of raster dataset.

* **Input:**

  * None

* **Output:**

  * Dictionary with raster parameters (`crs`, `transform`, `dtype`, `count`, `height`, `width`)

---

#### `rasterio.plot.show()`

**Description:** Displays raster image.

* **Input:**

  * Raster array or dataset

* **Output:**

  * Visualization (plot)

---

#### `rasterio.mask.mask()`

**Description:** Clips or masks raster using vector geometry.

* **Input:**

  * Raster dataset
  * Geometry list in GeoJSON-like format
  * `crop=True/False`
  * Optional `nodata` value

* **Output:**

  * Masked or clipped raster array
  * Updated affine transform

---

#### `rasterio.features.geometry_mask()`

**Description:** Creates a raster mask from vector geometries.

* **Input:**

  * Geometries
  * Transform
  * Output shape
  * Optional `invert=True/False`

* **Output:**

  * Boolean NumPy mask array

---

#### `rasterio.merge.merge()`

**Description:** Merges several raster datasets into one mosaic.

* **Input:**

  * List of opened raster datasets
  * Optional bounds, resolution, nodata, method

* **Output:**

  * Mosaic array
  * Output transform

---

#### `rasterio.windows.from_bounds()`

**Description:** Creates a raster window from geographic bounds.

* **Input:**

  * `left`, `bottom`, `right`, `top`
  * Raster transform

* **Output:**

  * Raster window object

---

#### `dataset.write()`

**Description:** Writes array data into a raster file.

* **Input:**

  * NumPy array
  * Band index or full stack
  * Output dataset opened in write mode

* **Output:**

  * Saved raster file

---

### GeoPandas Functions

#### `geopandas.read_file()`

**Description:** Loads vector data.

* **Input:**

  * File path (Shapefile, GeoJSON, etc.)

* **Output:**

  * GeoDataFrame

---

#### `GeoDataFrame.head()`

**Description:** Displays first rows of data.

* **Input:**

  * Number of rows (optional)

* **Output:**

  * Preview of GeoDataFrame

---

#### `GeoDataFrame.plot()`

**Description:** Plots vector geometries.

* **Input:**

  * Optional styling parameters

* **Output:**

  * Visualization (map)

---

#### `GeoDataFrame.to_crs()`

**Description:** Reprojects geometries to another CRS.

* **Input:**

  * Target CRS

* **Output:**

  * Reprojected GeoDataFrame

---

#### `GeoDataFrame.geometry`

**Description:** Accesses geometry column.

* **Input:**

  * None

* **Output:**

  * Geometry series

---

#### `GeoDataFrame.bounds`

**Description:** Returns bounding boxes of geometries.

* **Input:**

  * None

* **Output:**

  * DataFrame with `minx`, `miny`, `maxx`, `maxy`

---

#### `geopandas.clip()`

**Description:** Clips vector features by mask geometry.

* **Input:**

  * Input GeoDataFrame
  * Mask GeoDataFrame or polygon geometry

* **Output:**

  * Clipped GeoDataFrame

---

#### `GeoDataFrame.overlay()`

**Description:** Performs overlay operations between vector layers.

* **Input:**

  * Two GeoDataFrames
  * Operation type (`intersection`, `union`, `difference`, etc.)

* **Output:**

  * New GeoDataFrame with overlay result

---

#### `GeoDataFrame.to_file()`

**Description:** Saves vector data to file.

* **Input:**

  * Output path
  * Optional driver (`ESRI Shapefile`, `GeoJSON`, etc.)

* **Output:**

  * Saved vector file

---

## Clipping Pipelines

### Raster Clipping Pipeline

**Description:** Clips raster data using vector geometry.

**Main functions:**

* `geopandas.read_file()`
* `GeoDataFrame.to_crs()`
* `rasterio.open()`
* `rasterio.mask.mask()`
* `dataset.meta`
* `dataset.write()`

**Input:**

* Raster file (`.tif`)
* Vector mask (`.shp`, `.geojson`)

**Output:**

* Clipped raster array
* Updated transform
* Saved clipped raster file

---

### Vector Clipping Pipeline

**Description:** Clips one vector layer by another vector layer.

**Main functions:**

* `geopandas.read_file()`
* `GeoDataFrame.to_crs()`
* `geopandas.clip()`
* `GeoDataFrame.to_file()`

**Input:**

* Input GeoDataFrame
* Mask GeoDataFrame

**Output:**

* Clipped GeoDataFrame
* Saved vector file

---

## Mosaicing Pipeline

### Raster Mosaicing Pipeline

**Description:** Combines several raster scenes into one raster mosaic.

**Main functions:**

* `rasterio.open()`
* `rasterio.merge.merge()`
* `dataset.meta`
* `dataset.write()`

**Input:**

* List of raster files with matching CRS and compatible resolution

**Output:**

* Mosaic array
* New affine transform
* Saved mosaic raster

---

## Combined Operations

### Raster-Vector Integration

**Description:** Uses vector geometries to mask or clip raster data.

* **Input:**

  * Raster dataset
  * GeoDataFrame geometries

* **Output:**

  * Cropped or masked raster

---

### Spatial Selection / Overlay

**Description:** Selects or combines spatial features based on geometry relationships.

* **Input:**

  * One or more GeoDataFrames
  * Spatial condition or overlay rule

* **Output:**

  * Filtered or combined GeoDataFrame

---

## Outcome

* Ability to read and process raster data
* Ability to work with vector data
* Perform raster-vector integration
* Create clipped raster and vector datasets
* Build mosaics from several raster scenes

---

## Resources

* Rasterio Docs: [https://rasterio.readthedocs.io](https://rasterio.readthedocs.io)
* GeoPandas Docs: [https://geopandas.org](https://geopandas.org)


