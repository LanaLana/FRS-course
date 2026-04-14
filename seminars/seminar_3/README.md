# Seminar 3 — Sentinel Hub API: Data Download

## Overview
This seminar introduces how to work with the **Sentinel Hub API** for downloading satellite imagery programmatically.  
It focuses on automating data access, defining areas of interest, and retrieving multispectral data without using graphical interfaces.

---

## Objectives
- Understand how Sentinel Hub API works  
- Authenticate and configure API access  
- Define area of interest (AOI)  
- Request satellite imagery programmatically  
- Download and save raster data  
- Work with responses in Python  

---

## Structure
```
seminar_3/
│
├── Seminar_3_sh_api.ipynb
│
├── data/
│ └── (downloaded imagery)
│
└── README.md
```

- **notebook/** — step-by-step API usage and examples  
- **data/** — folder to download your requests  
- **README.md** — instructions  

---

## !Important!
- **Sentinel Hub doesn't allow you to download images larger than 2500 x 2500.**
- **You may not be able to download data from Google Collab.**
- **You can either download image directly to your pc memory on the temporal depending on the settings you configure.**

---

## Setup

### Install dependencies
```bash
pip install sentinelhub
```
---
### Create Sentinel Hub account
https://apps.sentinel-hub.com/

---
### Configure credentials
- Create OAuth client (client ID & secret)
- Save credentials locally or use config file

---
### Data Source
Sentinel Hub API (Sentinel-1/2 imagery and their derivatives)

---

### Workflow

1. Authenticate using Sentinel Hub credentials
2. Define area of interest (AOI)
3. Specify time range
4. Select dataset (Sentinel-2)
5. Configure request (bands, resolution, format)
6. Send request via API
7. Download and save result

---

## Example Analysis

Typical request parameters:

- Dataset: Sentinel-2 L2A
- Bands: B02, B03, B04, B08
- Resolution: 10–20 m
- Output: GeoTIFF or PNG

---

## How to?

### Tool Instruction — Authentication

1. Import required libraries (`sentinelhub`)
2. Set up configuration:

   * Client ID
   * Client secret
3. Initialize configuration object

---

### Tool Instruction — Define Area of Interest (AOI)

1. Specify bounding box coordinates
2. Define coordinate reference system (e.g., WGS84)
3. Create AOI object in code

---

### Tool Instruction — Create API Request

1. Define:

   * Time interval
   * Dataset (Sentinel-2 L2A)
2. Select bands (e.g., B02, B03, B04, B08)
3. Set resolution and image size
4. Define output format (GeoTIFF/PNG)

---

### Tool Instruction — Send Request

1. Create request object
2. Execute request
3. Retrieve response data

---

### Tool Instruction — Save Data

The method `get_data()` will always return a list of length 1 with the available image from the requested time interval in the form of numpy arrays.

If you want to save image, use `get_data(save_data=True)` 

---

## Outcome

* Downloaded satellite image via API
* Saved raster file (GeoTIFF/PNG)
* Basic visualization in Python

---

## Resources

* Sentinel Hub Docs: [https://docs.sentinel-hub.com](https://docs.sentinel-hub.com)
* Sentinel Hub Python package: [https://sentinelhub-py.readthedocs.io](https://sentinelhub-py.readthedocs.io)
