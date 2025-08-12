# 🌧️ Rainfall Prediction in Varanasi Region  
**Python | Machine Learning | Deep Learning**

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)  
[![Libraries](https://img.shields.io/badge/Libraries-NumPy%2C%20Pandas%2C%20Scikit--Learn%2C%20TensorFlow%2C%20Matplotlib%2C%20Seaborn-green.svg)](https://pypi.org/)  
[![Data Source](https://img.shields.io/badge/Data-ERA5%20Copernicus-orange.svg)](https://cds.climate.copernicus.eu/)  

## 📌 Project Overview
This project predicts **precipitation (rainfall)** in the **Varanasi region** using weather reanalysis data from **ERA5 Copernicus**.  
The pipeline covers **data preprocessing**, **feature engineering**, **exploratory data analysis (EDA)**, and **model training** using:
- **Decision Tree**
- **Random Forest**
- **k-Nearest Neighbors (k-NN)**
- **Long Short-Term Memory (LSTM)** deep learning model

The work was done in collaboration with the **Geophysics Department, Banaras Hindu University (BHU)**.

---

## 📂 Dataset
**Source:** ERA5 Copernicus Climate Data (NetCDF)  
**Processing:** Data extracted & converted to CSV in Linux environment.  
**Size:** 13,500 records × 13 columns.  
**Target Variable:** `tp` — Total precipitation (mm).  

### Example Data:
| time              | lon  | lat   | 100u   | 100v   | 10u    | 10v    | 2t     | e        | sp       | tp          | r     | z       |
|-------------------|------|-------|--------|--------|--------|--------|--------|----------|----------|-------------|-------|---------|
| 01-06-2000 10:00  | 82.5 | 25.50 | 1.3243 | -2.6790| 0.9875 | -2.2628| 310.99 | -0.00020 | 98718.48 | 1.91e-06    | 43.45 | 1914.32 |
| 01-06-2000 10:00  | 82.5 | 25.25 | 1.8751 | -2.8674| 1.4514 | -2.3858| 311.29 | -0.00019 | 98525.48 | 9.54e-07    | 40.92 | 1905.94 |

---

## 🛠 Workflow
### **1. Data Preprocessing**
- Loaded CSV data from ERA5 Copernicus output.
- Converted `time` to `datetime` and extracted:
  - `year`, `month`, `day`, `day_of_week`, `hour`
  - **Cyclic encoding**: `month_sin`, `month_cos`, `day_of_week_sin`, `day_of_week_cos`
- Handled missing values (none found in dataset).

### **2. Exploratory Data Analysis (EDA)**
- **Spatial grid mapping** of longitude-latitude points.
- **Time series** of rows per timestamp.
- **Distributions & outliers** (histograms, boxplots).
- **Correlation analysis** — Pearson correlation between `tp` and `r` ≈ **0.42**.

### **3. Feature Scaling**
- Used `StandardScaler` on all numerical features.
- Train-test split: **80% train / 20% test**.

### **4. Models Implemented**
#### ✅ Decision Tree Regressor
- `random_state=42`
- **R² = 0.8747**

#### ✅ Random Forest Regressor
- Tuned `n_estimators`, `max_depth` via GridSearchCV
- **R² = 0.8992** (Best performer among classical ML models)

#### ✅ k-Nearest Neighbors (k-NN)
- Tuned `n_neighbors` = 5–20
- **R² = 0.3234**

#### ✅ LSTM Deep Learning Model
- **Architecture:**
  - Multiple stacked LSTM layers (128 → 128 → 64 → 64 → 32 → 32)
  - Dropout layers (0.2)
  - Dense layers for regression output
- Optimizer: **Adam** (`lr=0.0005`)
- Loss: **MSE**
- EarlyStopping with patience=10
- **R² = 0.5487**

---

## 🔍 Hyperparameter Tuning
### **Decision Tree & Random Forest:**
Used **GridSearchCV** to optimize:
- `max_depth`
- `min_samples_split`
- `min_samples_leaf`
- `n_estimators` (RF)

### **k-NN:**
- Tuned `n_neighbors`, `weights`, `metric`.

### **LSTM:**
- Adjusted:
  - Number of layers & units per layer
  - Dropout rates
  - Batch size (16–64)
  - Learning rate (`0.0001–0.001`)
  - Epoch count (EarlyStopping prevented overfitting)

---

## 📊 Results Summary
| Model            | MSE          | MAE          | R² Score   |
|------------------|--------------|--------------|------------|
| Decision Tree    | 5.21e-08     | 3.11e-05     | **0.8747** |
| Random Forest    | 4.19e-08     | 6.79e-05     | **0.8992** |
| k-NN             | ~0.0000      | 0.0002       | 0.3234     |
| LSTM             | 0.0023       | 0.0192       | 0.5487     |

---

## 📈 Key Visualizations
- **Spatial grid** of measurement points  
- **Time series** of dataset completeness  
- **Correlation heatmap** of variables  
- **Precipitation vs Relative Humidity** scatter plot  
- **Distribution plots & boxplots** for all features  

---

## 🚀 Future Improvements
- Incorporate **more historical data** for better LSTM training.
- Explore **XGBoost & LightGBM** for boosted tree performance.
- Experiment with **hybrid ML + deep learning ensemble**.

---


Author: SK Samim Ali
M.Sc. Computational Science & Applications (Data Science Specialization) — Banaras Hindu University
📧 Email: roy871858@gmail.com
