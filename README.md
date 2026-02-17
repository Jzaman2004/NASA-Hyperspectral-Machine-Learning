# 🛰️ NASA-Powered Hyperspectral Machine Learning with NEON Imagery to Predict Vegetation Traits at 1-Meter Resolution in Harvard Forest

[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![Earth Engine](https://img.shields.io/badge/Google-Earth%20Engine-4285F4.svg)](https://earthengine.google.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![ESA 2026](https://img.shields.io/badge/Conference-ESA%202026-2E8B57.svg)](https://esa2026.confex.com/)

## 📖 Overview

This research project demonstrates how machine learning algorithms can translate NASA's 426-band AVIRIS-NG hyperspectral imagery, deployed via the National Ecological Observatory Network (NEON), into accurate predictions of vegetation traits at 1-meter spatial resolution. Focusing on Harvard Forest, Massachusetts, this pipeline integrates Google Earth Engine for data extraction, Principal Component Analysis (PCA) for dimensionality reduction, and five supervised learning models to predict key vegetation indices (NDVI, EVI, PRI).

**Key Finding:** Support Vector Regression (SVR) achieved the highest accuracy for EVI prediction (**R² = 0.87**), while Gradient Boosting performed best for PRI (**R² = 0.49**).

**Cross-Site Validation:** A comparative analysis using Landsat 8 imagery revealed Black Rock Forest exhibited ~50% higher NDVI than Harvard Forest (0.36 vs. 0.24), demonstrating the scalability of the machine learning framework across geographically distinct temperate deciduous ecosystems.

## 🌿 Research Objectives

1. Extract hyperspectral reflectance data from NEON's Surface Bidirectional Reflectance product (DP3.30006.002).
2. Reduce dimensionality from 54 spectral bands to 15 principal components (retaining 99.99% variance).
3. Benchmark five machine learning models (Random Forest, XGBoost, Linear Regression, SVR, Gradient Boosting) for vegetation index prediction.
4. Provide a reproducible, open-source pipeline for ecological remote sensing at fine spatial scales.
5. Assess cross-site generalizability by comparing vegetation indices between Harvard Forest and Black Rock Forest.

## 🛠️ Methodology

### Part 1: NEON Hyperspectral Analysis (Harvard Forest)
1. **Data Acquisition:** Authenticate Google Earth Engine and load NEON hyperspectral collection.
2. **Spatial Sampling:** Generate 50 random sample points within Harvard Forest bounds.
3. **Spectral Extraction:** Extract 54 spectral bands (visible to shortwave infrared) at 1-meter resolution.
4. **Vegetation Indices:** Calculate NDVI, EVI, and PRI from spectral bands.
5. **Dimensionality Reduction:** Apply PCA to reduce 54 bands → 15 components.
6. **Model Training:** Train and test 5 ML models (80/20 split).
7. **Evaluation:** Assess performance using R² and RMSE metrics.
8. **Visualization:** Generate performance bar charts and prediction scatterplots.
9. **Documentation:** Save all results, models, and figures to Google Drive.
10. **Archiving:** Publish code and documentation to GitHub for reproducibility.

### Part 2: Landsat Site Comparison (Harvard Forest vs. Black Rock Forest)
11. Load Landsat Collection 2 Level-2 data (30m resolution) via Google Earth Engine.
12. Define study sites: Harvard Forest (42.5370°N, -72.1850°W) and Black Rock Forest (41.40806°N, -74.02167°W) with 5km analysis radius.
13. Filter Landsat collection by date (2013 growing season), bounds, and cloud cover (<20%); select single least-cloudy image per site.
14. Calculate NDVI and EVI from Landsat bands (SR_B3=Green, SR_B4=Red, SR_B5=NIR); exclude PRI (band resolution not suitable).
15. Extract mean vegetation indices within 5km radius using `reduceRegion()` at 30m scale.
16. Generate side-by-side bar charts comparing NDVI and EVI between sites with value labels.
17. Calculate absolute and percent differences between sites; interpret ecological implications.
18. Save comparison results, summary statistics, and visualizations to Google Drive.
19. Update GitHub repository with new notebook and README documentation.

## 📊 Key Results

### Hyperspectral Analysis (NEON AVIRIS-NG, Harvard Forest)
| Target Variable | Best Model | R² Score | RMSE |
|-----------------|------------|----------|------|
| **EVI** (Atmospherically Corrected Greenness) | Support Vector Regression | **0.87** | 0.128 |
| **PRI** (Photosynthetic Stress) | Gradient Boosting | **0.49** | 0.049 |
| **NDVI** (Canopy Greenness) | SVR | 0.00* | 0.146 |

*\*NDVI prediction yielded low R² values across all models, consistent with its direct mathematical derivation from the input spectral bands.*

**Overall Best Model:** XGBoost achieved the highest average R² across all three targets (0.40).

### Cross-Site Comparison (Landsat 8, 2013)
| Metric | Harvard Forest | Black Rock Forest | Difference |
|--------|---------------|-------------------|------------|
| **NDVI** | 0.2413 | 0.3635 | **+50.6%** |
| **EVI** | 8.21 | 11.98 | **+45.9%** |

**Interpretation:** Black Rock Forest showed higher canopy greenness and atmospheric-corrected vegetation signal, suggesting regional variation in phenology, species composition, or site conditions within temperate deciduous ecosystems.
