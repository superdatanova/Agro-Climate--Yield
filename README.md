# 🌾 Agro Climate Yield: Smart & Sustainable Agriculture

## 📌 Project Overview

This project presents a **robust and unique** approach to develop a smart decision-making system for agriculture by **integrating unsupervised learning (clustering) with supervised regression techniques** to accurately predict crop yield. The goal is to understand how environmental conditions, pesticide use, and crop types influence yield—and to promote sustainable farming practices. Agriculture is deeply influenced by the environment. Rainfall, temperature, and pesticide use vary dramatically across regions—and so does crop productivity. This project explores how these factors interact to shape crop yield, using data science to **uncover patterns and build predictive tools that support smarter, more sustainable farming.**


---

## 🗂️ Dataset

- **Source:** [Kaggle Crop Yield Dataset](https://www.kaggle.com/code/patelris/crop-yield-eda-viz/notebook)  
- **Derived From:**  
  - [FAO – Food and Agriculture Organization](http://www.fao.org/home/en/)  
  - [World Bank Open Data](https://data.worldbank.org/)  

> Includes data on crop yield, rainfall, temperature, pesticide usage, crop types, and regions across multiple years.

---

## 🎯 Project Goals (NON-TECHNICAL EXPLANATION OF THE PROJECT)

- Develop a predictive model for crop yield based on environmental and agricultural inputs  
- Identify key factors influencing yield to support targeted interventions  
- Advance sustainable farming through data-driven insights  
- Define agro-climatic zones to enable region-specific agricultural strategies  

The main goal is to combine **unsupervised learning** (clustering) with **supervised regression** to build a smart, adaptive system for agricultural decision-making. The model leverages climate and farming data to estimate expected harvests and uncover the most influential variables affecting yield.

To enhance interpretability and relevance, new metrics were introduced:
- **Yield per pesticide used**: Measures efficiency of chemical input  
- **Rainfall-to-temperature ratio**: Captures environmental balance  
- **Agro-climatic zones**: Groups regions by climate and input patterns for localized insights  

These findings can guide practical decisions—such as optimizing pesticide use, selecting suitable crops for specific zones, and understanding how environmental conditions shape productivity.  

Imagine a farmer in a tropical zone with high rainfall and warm temperatures, using minimal pesticides. Compare that to one in a cold, dry region relying heavily on chemical inputs. How do their yields differ? What practices lead to better outcomes?  



---
## Who It's For

- **Farmers** seeking to optimize inputs and improve harvests  
- **Agronomists** analyzing crop performance across regions  
- **Policy makers** designing climate-resilient agricultural programs  
- **Researchers** exploring sustainable farming practices  

This project helps answer those questions—empowering farmers, agronomists, and policymakers with actionable, data-driven knowledge.

---

## ⚙️ How It Works

This project integrates diverse datasets to build a robust analytical framework for agricultural forecasting. Key data sources include:

- **Climatic variables**: Regional rainfall and temperature patterns, tracked annually  
- **Agricultural inputs**: Pesticide usage data by region and year  
- **Crop yield records**: Historical yield data across multiple countries and crop types  

By synthesizing these inputs, the model uncovers relationships between environmental conditions, farming practices, and crop productivity—laying the foundation for predictive insights and strategic interventions.

## 🔄 Methodology overview
## The two-stage process:
**Unsupervised Clustering:** I used K-Means to identify distinct agro_zones based on environmental factors and pesticide use, and this feature was added to the dataset. 
**Supervised Regression:** I compared 3 different regression models (Ridge, RF, GB) to predict yield, incorporating the agro_zone feature along with other relevant factors like yield per pesticide used and rainfall-to-temperature ratio—to better assess farming efficiency and environmental impact.

### 1. 📊 Data Preparation & Exploration

- Cleaned and merged datasets  
- Performed EDA to understand distributions  
- Applied log transformation to normalize skewed yield values

<img width="1382" height="683" alt="image" src="https://github.com/user-attachments/assets/5ca796a6-b7c6-4b41-afd9-4dc260b0af46" />


### 2. 🧭 Unsupervised Clustering – Agro Zones

Used **K-Means clustering** to group regions based on climate and pesticide use:

| Zone | Description |
|------|-------------|
| 0 | Tropical, high rainfall & temperature, low pesticide use (possibly organic) |
| 1 | Cold & dry, low-input farming |
| 2 | Balanced climate, high pesticide use (intensive farming) |
| 3 | Hot & dry, drought-resistant crops |
| 4 | High input zone, industrial-scale farming |

They capture the interactions between rainfall, temperature, and pesticide use in a non-linear way that clustering reveals. For example, within a high-pesticide zone, the impact of temperature might be different than in a low-pesticide zone, and the agro_zone feature can help the model learn these nuances. Very helpful for future analysis.

<img width="843" height="682" alt="image" src="https://github.com/user-attachments/assets/cfce12ba-af29-480b-bc11-da606daa0a5f" />


### 3. 📐 Feature Engineering

- Created new metrics:
  - `yield_per_pesticide`  
  - `rainfall_temp_ratio`  
- One-hot encoded categorical features including `agro_zone`

View Feature Dependency Heatmap
<img width="1374" height="743" alt="image" src="https://github.com/user-attachments/assets/0b16e2c8-02d2-4bf7-836a-9409c2bccb9d" />

### 4. 🤖 Supervised Regression Modeling

Trained and evaluated three models:

- Ridge Regression  
- Random Forest  
- Gradient Boosting (GB)  

> **Gradient Boosting** showed the best performance in predicting the crop yield.


<img width="711" height="562" alt="image" src="https://github.com/user-attachments/assets/22b5aacf-03fd-4ec1-8f0f-aa6b758b8d86" />

<img width="704" height="561" alt="image" src="https://github.com/user-attachments/assets/b7799aba-1968-4b3f-b4fd-139de5c6a879" />


<img width="722" height="572" alt="image" src="https://github.com/user-attachments/assets/d88b6a8f-52c6-4b2a-a6c6-7c374f1b38cc" />




### 5. 🔧 Hyperparameter Tuning

Used **Optuna** with **TPESampler** (Bayesian optimization) to fine-tune Gradient Boosting:

- Improved R² score and reduced RMSE  
- Enhanced generalization and model stability

---

### 6. 🧠 Model Interpretation: SHAP Analysis

To enhance transparency and interpretability, SHAP (SHapley Additive exPlanations) was applied to the Gradient Boosting model. This approach quantifies the contribution of each feature to individual predictions, offering clear insights into model behavior.

### 📊 Top Influential Features

- **Pesticides (tonnes)**: Strongly correlated with yield outcomes, highlighting the impact of chemical inputs  
- **Yield per pesticide**: A derived efficiency metric that proved highly predictive  
- **Crop type**: Certain crops, such as **Potatoes**, exhibited distinct yield patterns  
- **Agro-climatic zone features**: Captured regional variability, contributing significantly to prediction accuracy  

SHAP analysis confirmed that both environmental and agricultural variables play critical roles in determining crop yield. These insights support more informed, localized decision-making in agricultural planning.

![image.png](attachment:0ad07b38-6e05-47ff-a28e-a19580b271b0.png).
---

## ✅ Key Insights

- **Pesticide usage** and **efficiency metrics** are dominant yield drivers  
- **Agro-zones** help capture hidden environmental patterns  
- **Crop type** significantly affects yield outcomes  
- Model supports **localized recommendations** for crop selection and input optimization

---

## 🌱 Contribution to Smart & Sustainable Agriculture

- Predict yield under varying conditions  
- Optimize pesticide use for better yield and lower environmental impact  
- Identify resilient crops for specific agro-zones  
- Support data-driven decisions for sustainable farming

---

## ⚙️ Technical Highlights

- Log transformation of skewed target variable  
- One-hot encoding of categorical features  
- Optuna-based hyperparameter tuning  
- SHAP for model explainability

---

## 🚀 How to Use

- Run the notebook: `Part2_MM_25_3_Portfolio_Project.ipynb`  
- Preprocessing steps: `Part1_MM_25_3_Portfolio_Project.ipynb`  
- View model overview: `Overview_of_the_main_Model_Python_file.md`  
- Access final dataset: `final_crop_yield_data.csv`

---
## Impact

This model helps uncover which combinations of climate and agricultural inputs lead to better yields. It supports:

- **Smarter resource use** (e.g., reducing pesticide without sacrificing productivity)  
- **Localized recommendations** based on agro-zone characteristics  
- **Sustainable planning** in the face of climate variability  

Whether you're growing rice in a humid zone or wheat in a dry one, this tool offers insights to guide decisions and improve outcomes.

## 🔗 Additional Resources


- [📈 Link to Main Model Building Code](Part2_MM_25_3_Portfolio_Project.ipynb)  
- [📋 Model Card](model_card.md)  
- [📄 Data Sheet](data_sheet.md)

---

## 🔮 Future Directions

- Integrate **soil quality and fertilizer composition**  
- Add **satellite imagery** for spatial analysis  
- Model **long-term climate trends**  
- Promote **eco-friendly and resilient agriculture** through localized recommendations
