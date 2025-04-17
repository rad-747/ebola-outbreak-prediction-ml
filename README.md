# 🧬 Predicting Ebola Outbreak Metrics using Machine Learning  
*A Submission for the IIT Bombay ML Challenge*

This project focuses on predicting critical metrics related to Ebola outbreaks — **Deaths**, **Case Fatality Ratio (CFR)**, and **Confirmed Cases** — using geospatial data and machine learning models. The solution was developed and submitted for the **TopG ML competition** hosted by **IIT Bombay**.

---

##  Project Overview

Ebola outbreaks pose a serious public health challenge. To support early intervention and resource allocation, this project leverages machine learning to:

- Predict **deaths** using spatial and environmental features
- Estimate **CFR** based on regional and fatality data
- Derive **confirmed cases** using predictions and medical heuristics

---

##  Dataset Description

The dataset includes spatial and outbreak-related features:

| Feature Name           | Description                                                  |
|------------------------|--------------------------------------------------------------|
| `Lat`, `Long_`         | Geographic coordinates of the outbreak                      |
| `Deaths`               | Number of deaths in each region (partially missing)         |
| `Case_Fatality_Ratio`  | Deaths ÷ Confirmed Cases × 100                              |
| `Confirmed_Cases`      | Calculated using predicted values                           |

---

##  Methodology

###  Data Cleaning
- Removed invalid latitude and longitude values (outside -90 to 90 and -180 to 180).
- Dropped rows with missing spatial coordinates.
- Handled extreme outliers in `Case_Fatality_Ratio` using 3-sigma rule.

### Feature Engineering
- `Distance_Equator = abs(Lat)`
- `Lat_Long_Interaction = Lat × Long_`
- `Region` buckets created using `Lat // 10`

###  EDA Visuals
- Histogram and box plot of CFR
- Correlation heatmap
- Deaths vs. Distance from Equator
- Geographical scatter plot of points (Plotly)

---

##  Machine Learning Pipeline

###  Imputation
- **XGBoost Regressor** was used to impute missing `Deaths` values.
- Rounded predicted values to maintain consistency.

###  Modeling

#### 1. LightGBM for Deaths
- **Features**: `Lat`, `Long_`
- **Training RMSE**: 31.19  
- **Validation RMSE**: 34.11

#### 2. LightGBM for Case Fatality Ratio (CFR)
- **Features**: `Lat`, `Long_`, `Deaths`, `Region`
- **Training RMSE**: 0.51  
- **Validation RMSE**: 0.71

---


