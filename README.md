# Explainable Machine Learning Reveals Water-Related Drivers of Sub-Field Dryland Wheat Yield Variability

Code repository accompanying the manuscript:

**Lamichhane, M., Mehan, S., Mankin, K.R., Trooien, T., Maimaitijiang, M., Moradi Rekabdarkolaee, H.** *Explainable machine learning reveals water-related drivers of sub-field dryland wheat yield variability.*

## Overview

This repository contains the data-preprocessing and modeling pipeline used to identify and quantify the controls on sub-field-scale dryland wheat yield variability across 18 fields in northeastern Colorado (2019–2024). The workflow combines:

- Remote-sensing-derived actual evapotranspiration (ETa)
- Soil moisture (SM)
- Precipitation, soil properties, and topographic features
- XGBoost regression models under eight feature-set combinations
- SHAP (SHapley Additive exPlanations) analysis for model interpretability
- Temporal- and spatial-blocking cross-validation

Models were evaluated under both aspirational (ASP; no-till, diversified rotation) and business-as-usual (BAU; reduced tillage, wheat–fallow) management systems.

## Repository Structure

```
.
├── notebooks/
│   ├── 01_ETa_Data_Preprocessing.ipynb        # Monthly aggregation, 5 m resampling & DEM alignment for ETa
│   ├── 02_Soil_Moisture_Data_Preprocessing.ipynb  # Monthly aggregation, resampling & alignment for soil moisture
│   └── 03_ML_Models_Pipelines.ipynb           # XGBoost feature-set experiments, SHAP analysis, temporal & spatial blocking
├── data/
│   ├── raw/                                   # Place input rasters/vectors here (not tracked in git — see .gitignore)
│   └── processed/                             # Intermediate preprocessed outputs
├── results/                                   # Model outputs, figures, and summary tables
├── requirements.txt
└── .gitignore
```

## Getting Started

### 1. Environment setup

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

> **Note on GDAL/rioxarray:** `osgeo.gdal` and `rioxarray` can be difficult to install via plain `pip` on Windows. If `pip install` fails, install these via conda instead:
> ```bash
> conda install -c conda-forge gdal rioxarray xarray
> ```

### 2. Data

Raw and processed raster/vector data are **not included** in this repository (see `.gitignore`). Each notebook's early cells define input/output folder paths — update these to point to your local `data/raw/...` and `data/processed/...` locations (or your own directory structure) before running.

### 3. Run order

1. `01_ETa_Data_Preprocessing.ipynb`
2. `02_Soil_Moisture_Data_Preprocessing.ipynb`
3. `03_ML_Models_Pipelines.ipynb`

## Methods Summary

Eighteen dryland wheat fields were grouped into ASP and BAU management systems. XGBoost models were trained across eight feature combinations (precipitation, soil moisture, ETa, soil properties, topography, and combinations thereof). Model performance was assessed under both random partitioning and field-level holdout. SHAP values were used to attribute yield variability to specific biophysical drivers, with early-season water-related variables (particularly ETa) identified as the most spatially informative predictors of yield.

## Citation

If you use this code, please cite the associated manuscript (citation to be finalized upon publication).

## Contact

- Manoj Lamichhane — Department of Agricultural and Biosystems Engineering, South Dakota State University
- Sushant Mehan — Department of Agricultural and Biosystems Engineering, South Dakota State University

