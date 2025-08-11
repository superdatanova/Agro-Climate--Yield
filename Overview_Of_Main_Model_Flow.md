# 🌾 Crop Yield Prediction Model Overview

## 🎯 Objective
The main goal of this project is to predict crop yield based on environmental and agricultural factors. The approach combines:
- **Unsupervised learning (clustering)** to create a new feature called `agro_zone`
- **Supervised regression modeling** to predict yield using this new feature and others

---

## ❓ Problem Statement
Build a predictive model that accurately estimates crop yield given:
- Environmental conditions
- Agricultural practices (e.g., pesticide use)
- Crop type

Challenges:
- Skewed distribution of yield data
- Need to uncover patterns in environmental/agricultural data to improve predictions

---

## 🧠 Code Outline

### 1. Setup and Data Loading
- Import necessary libraries
- Load `final_crop_yield_data.csv` into a pandas DataFrame

### 2. Pre-Clustering Exploratory Data Analysis (EDA)
- Preview and describe raw data
- Visualize distributions using histograms and boxplots for:
  - `average_rain_fall_mm_per_year`
  - `avg_temp`
  - `pesticides_tonnes`
  - `yield`
- Generate correlation heatmap (features weakly correlated)
- Apply PCA to assess dimensionality
- Demonstrate Central Limit Theorem using `yield` samples

### 3. Clustering to Create `agro_zone`
- Apply K-Means clustering on:
  - `average_rain_fall_mm_per_year`
  - `avg_temp`
  - `pesticides_tonnes`
- Use Elbow Method to determine optimal clusters (≈5)
- Fit K-Means and add `agro_zone` column
- Visualize clusters using PCA
- Normalize and interpret agro-zone characteristics

### 4. Feature Engineering
Create new features:
- `yield_per_pesticide`: Efficiency of pesticide use
- `rainfall_temp_ratio`: Rainfall vs. temperature relationship
- `year_group`: Temporal binning of years

Encode categorical features:
- One-Hot Encode: `year_group`, `item`, `agro_zone`

### 5. Post-Clustering EDA
- Check DataFrame shape, types, and missing values
- Visualize `yield` distribution (positively skewed)
- Apply `log1p` transformation to `yield`
- Convert boolean columns to integers
- Generate final correlation heatmap

### 6. Model Building
- Split data into training/testing sets
- Target `y`: `log_yield`
- Features `X`: Numerical, engineered, and one-hot encoded features

Models used:
- Ridge Regression (with StandardScaler pipeline)
- Random Forest Regressor
- Gradient Boosting Regressor

Define `evaluate_model` function:
- Train model
- Predict and inverse log transform
- Evaluate using R², RMSE, MAE

Apply KFold cross-validation  
Plot learning curves (Gradient Boosting shows promise)

### 7. Hyperparameter Tuning with Optuna
- Use Optuna to optimize Gradient Boosting hyperparameters
- Print best parameters

### 8. Model Interpretation with SHAP
- Use SHAP to analyze feature importance
- Generate:
  - SHAP summary plot
  - SHAP bar plot
- Interpret key features influencing crop yield

---

## 📊 Features and Target Summary

### 🔍 Unsupervised Learning (Clustering)
- **Features**: `average_rain_fall_mm_per_year`, `avg_temp`, `pesticides_tonnes`
- **Target**: None (goal is to discover patterns using clustering)
- **Output**: New categorical feature `agro_zone`

### 📈 Supervised Learning (Regression)
- **Features (X)**:
  - Original: `average_rain_fall_mm_per_year`, `avg_temp`, `pesticides_tonnes`, `year`
  - Engineered: `yield_per_pesticide`, `rainfall_temp_ratio`
  - One-Hot Encoded:
    - `year_group_1990–95` to `year_group_2011–15`
    - `item_Cassava` to `item_Yams`
    - `agro_zone_0` to `agro_zone_4`
  - Dropped: `area` (metadata, want to check distribution on agro_zone instead of area), `yield` (original target)

- **Target (y)**:
  - `log_yield` (log-transformed crop yield)
  - Transformation improves model performance and handles skewness

##  Related Files & Resources

- [📋 Link To ReadMe File](ReadMe.md) 
- [📈 Link to Main Model Building Code](Part2_MM_25_3_Portfolio_Project.ipynb)  
- [📋 Model Card](model_card.md)  
- [📄 Data Sheet](data_sheet.md)
- [📈 Link to overview of Main Model](Overview_Of_Main_Model_Flow.md) 
- [📈 Link to overview of Data Preprocessing](Overview_Of_Data__Pre-Processing.md)
- [📈 Link to Data Pre-Processing Code](Part1_MM_25_3_Portfolio_Project.ipynb) 
- [📋 Link to Main Data File](final_crop_yield_data.csv)
---

## 🧩 Summary
- Clustering revealed hidden structures (`agro_zones`)
- These zones enhanced regression model performance
- Log transformation of `yield` was essential for handling skewness