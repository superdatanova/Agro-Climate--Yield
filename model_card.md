#  Model Card: Crop Yield Prediction

##  Model Description

## Attribute Overview

| Attribute             | Details                              |
|----------------------|--------------------------------------|
| **Model Type**        | Gradient Boosting                    |
| **Training Size**     | 13,000+ records                      |
| **Evaluation Metrics**| R², RMSE, MAE                        |
| **Tuning Technique**  | Optuna (Bayesian Optimization)       |
| **Feature Importance**| SHAP Analysis                        |



## Input:  
The model takes in a combination of environmental and agricultural features, including:

- **Original features**:  
  - `year`  
  - `average_rain_fall_mm_per_year`  
  - `avg_temp`  
  - `pesticides_tonnes`  

- **Engineered features**:  
  - `yield_per_pesticide`  
  - `rainfall_temp_ratio`  

- **One-hot encoded features**:  
  - Year group dummies  
  - Crop type dummies  
  - Agro-climatic zone dummies  

-  **[Link to Data Preprocessing Code](Part1_MM_25_3_Portfolio_Project.ipynb)**

-  **[Link to Main Model Building Code](Part2_MM_25_3_Portfolio_Project.ipynb)**

-  **[Link to Main Data File](final_crop_yield_data.csv)**

-  **[Link to Read Me File](README.md)**
  

The data was sourced from four CSV files: yield.csv, rainfall.csv, temp.csv, and pesticides.csv. Each dataset was cleaned by standardizing column names, fixing data types, handling missing values, and removing outliers. Rainfall, temperature, and pesticide data were aggregated by area and year. Finally, all datasets were merged into a single, unified DataFrame for crop yield analysis.File name:final_crop_yield_data.csv

## Output: 
The model outputs a prediction for **log-transformed crop yield** (`log_yield`). To obtain the actual yield, the inverse transformation is applied using `np.expm1()`.

**Model Architecture:**  
The final model is a **Gradient Boosting Regressor**, selected after comparing performance with Ridge and Random Forest regressors. Hyperparameters were optimized using **Optuna** for best results.

---
## Model Details

The model is a **Gradient Boosting Regressor** trained to predict the log-transformed crop yield (`log_yield`). This model was selected after an initial evaluation of several supervised regression models (**Ridge Regression, Random Forest, and Gradient Boosting**) using features that included a newly engineered `agro_zone` feature. This **feature** was derived through unsupervised **K-Means clustering** of environmental factors.

Among the initial candidates, the Gradient Boosting model demonstrated the best performance and was subsequently optimized using **Optuna - Bayesian optimisation approach** for hyperparameter tuning.

This solution is both **robust and uniquely tailored** to the complexities of agricultural data. By integrating unsupervised clustering with supervised regression, it captures latent environmental patterns and direct yield relationships simultaneously. Such a hybrid approach enhances predictive accuracy and interpretability, making it a valuable tool for guiding data-driven decisions in sustainable agriculture. It empowers stakeholders to better understand how environmental conditions and input usage affect crop productivity, ultimately supporting more resilient and efficient farming practices.

##  Performance

The **Gradient Boosting model** demonstrated superior predictive accuracy on the test set compared to other models. Performance was evaluated using:
Root Mean Squared Error (RMSE), R², and MAE

SHAP analysis was used to interpret model predictions, revealing the most influential features:

- `pesticides_tonnes`  
- `yield_per_pesticide`  
- Crop types (e.g., Potatoes)  
- Agro-climatic zone indicators  

These features significantly contributed to the model’s ability to capture regional and input-based variations in yield.

> **Gradient Boosting was selected based on learning curve behavior and tuning potential.**

- **Initial Metrics:** Random Forest had slightly better R², RMSE, and MAE.(RF R²: 0.978, GB : R²: 0.846)
- **Cross Validation Report** Random Forest - CV R²: 0.983 ± 0.001, Gradient Boosting - CV R²: 0.934 ± 0.002 – GB getting closer to RF
- **Bias–Variance Tradeoff & Learning Curves:**  
  - RF plateaued early—limited gain with more data.  
  - GB showed upward validation trend—indicating untapped potential with more data or hyper parameter tuning
- **Model Sensitivity:**  
  - GB is more responsive to hyperparameter tuning.  
  - RF performs well out-of-the-box but less tunable.
- **Optuna Optimization:**  
  - Tuned GB achieved **Best trial: R² Score: 0.9886 outperforming RF’s **R² ≈ 0.983**.  
  - Confirmed GB’s capacity for improvement.

---

##  Limitations

- The model predicts **log-transformed yield**, which requires post-processing to interpret in real-world units.  
- Predictions are only as reliable as the input data—missing or inaccurate records can affect performance.  
- Agro-climatic zones are derived from clustering and may oversimplify complex regional dynamics.  
- The model does not account for socio-economic factors, soil health, or farming practices beyond pesticide use.

---

##  Trade-offs

- **Generalization vs. Localization**: While agro-zones help tailor predictions, they may reduce granularity for hyper-local decisions.  
- **Interpretability vs. Complexity**: Gradient Boosting offers strong performance but is less interpretable than linear models—SHAP helps bridge this gap.  
- **Efficiency vs. Accuracy**: Feature engineering improves accuracy but adds complexity to preprocessing pipelines.

---

##  Summary

This model supports smart agricultural decision-making by predicting crop yield using a blend of environmental data, chemical inputs, and engineered features. It enables:

- Resource optimization (e.g., pesticide use)  
- Crop selection based on regional conditions  
- Insight into environmental drivers of productivity  

By combining unsupervised clustering (agro-zones) with supervised regression, the project offers a scalable and interpretable framework for data-driven farming.