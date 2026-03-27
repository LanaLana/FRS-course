# Seminar — MODIS Time Series Analysis with LSTM

## Overview
This seminar demonstrates how Long Short-Term Memory (LSTM) networks can be applied to remote sensing time series data.

Using MODIS NDVI (Normalized Difference Vegetation Index) data, the notebook walks through the full workflow of preparing sequential data and training a deep learning model to capture temporal patterns in vegetation dynamics.

---

## Objectives
- Understand MODIS NDVI time series data  
- Explore temporal satellite datasets  
- Perform preprocessing for sequential modeling  
- Construct time-series input sequences  
- Train an LSTM model for prediction  
- Evaluate model performance  
- Interpret temporal patterns in vegetation data  

---

## Structure

- MODIS_lstm.ipynb - jupyter notebook

- data.csv - dataset

- README_MODIS.md - this file

---

## Setup

### Install dependencies
pip install numpy pandas matplotlib torch scikit-learn

---

## Data Description

The dataset contains time series observations of NDVI values for multiple pixels.

Each record includes:
- time -- timestamp of observation  
- pixel -- spatial location ID  
- ndvi -- vegetation index value  
- qa -- quality flag  

---

## Workflow

1. Import required libraries  
2. Load MODIS NDVI dataset  
3. Explore and visualize time series  
4. Clean and preprocess data  
5. Construct sequences for LSTM input  
6. Split data into training and testing sets  
7. Build and train LSTM model  
8. Evaluate predictions  
9. Visualize model performance  

---

## Outcome

- Ability to work with satellite time series datasets  
- Prepare sequential data for deep learning  
- Train an LSTM model  
- Apply deep learning to remote sensing problems  

---
