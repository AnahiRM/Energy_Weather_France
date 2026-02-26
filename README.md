# 🌍 Energy Consumption under Changing Weather  
### A Machine Learning Case Study of French Energy Demand  

**Authors:** Anahí Reyes Miguel and Robert Campbell Powers

This project builds machine learning models to predict **daily regional electricity consumption per capita in France** using weather, demographic, and calendar data.  
It evaluates multiple models to understand the **non-linear relationship between weather patterns and energy demand** and to support energy planning in a renewable-transition context.

---

## Overview

Accurate electricity demand forecasting is essential for modern power grid management.  
With renewable energy production highly dependent on weather conditions, understanding how weather affects consumption is critical for grid stability, planning, and policy.

This project uses statistical learning methods to estimate regional electricity demand in France based on observed weather conditions.

Main objective:  
Predict **daily electricity consumption per capita** at the regional level using weather and demographic data.

---

## Dataset

The final dataset combines three sources:

### Electricity consumption  
**Source:** Opendata Réseaux-Énergies (ODRÉ)  
- Half-hourly regional consumption  
- Aggregated to daily totals  
- Metropolitan France (excluding Corsica)  
- Period used: 2014–2021  

### Weather data  
**Source:** Météo-France  
- 3,900+ weather stations  
- 200+ meteorological variables  
- Aggregated to daily regional averages  

### Population statistics  
**Source:** INSEE  
- Regional population (2014–2024)  
- Used to compute per-capita consumption  
- Population density constructed as additional feature  

---

## Final modeling dataset

- Unit: region × day  
- Rows: ~57,000  
- Features after cleaning: 29  
- Target: electricity consumption per capita  

Cleaning steps:
- Removed variables with >20% missing values  
- Removed multicollinearity using VIF threshold  
- Aggregated weather stations to regional averages  
- Constructed per-capita consumption  

---

## Repository Structure
```
Energy_Weather_France/
│
│── data/
│  ├── france_energy_meteo_daily.csv
│  ├── POPULATION_MUNICIPALE_REGION_FRANCE.xlsx
│
├── 01_data_cleaning.ipynb
├── 02_modeling.ipynb
│
├── output/
└── README.md
```

### Notebooks

**Data Cleaning.ipynb**
- Merge datasets  
- Feature engineering  
- Cleaning and preprocessing  

**ML Analysis.ipynb**
- Model training  
- Hyperparameter tuning  
- Evaluation and visualization  

---

## Methodology

We use a supervised regression framework to predict daily electricity consumption per capita.

### Models implemented
- Linear Regression (baseline)
- Decision Tree
- Random Forest
- Support Vector Regressor (RBF kernel)
- Multilayer Perceptron (MLP neural network)

### Pipeline

1. Merge weather, energy, and population data  
2. Create per-capita consumption target  
3. Train/test split (80/20 random split)  
4. Feature scaling for SVM and MLP  
5. Hyperparameter tuning using GridSearchCV  
6. Evaluation using:
   - MAE  
   - RMSE  
   - R²  

---

## Results

| Model | RMSE | MAE | R² |
|------|------|-----|----|
| Linear Regression | 4.38 | 5.50 | 0.68 |
| Decision Tree | 3.06 | 3.88 | 0.84 |
| Random Forest | **2.62** | **3.30** | **0.88** |
| SVM (RBF) | 3.04 | 3.90 | 0.84 |
| MLP Neural Network | 2.66 | 3.32 | 0.88 |

Random Forest and MLP provide the best predictive performance, improving RMSE by ~40% over the linear baseline.  
This confirms a strong **non-linear relationship between weather variables and electricity demand**.

Random Forest offers the best trade-off between performance and interpretability.

---

## How to Run

### Clone repository
```bash
git clone <repo_link>
cd Energy_Weather_France
