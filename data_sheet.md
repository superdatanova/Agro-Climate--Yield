#  Datasheet: Crop Yield Prediction Dataset

---

##  Motivation

- **Purpose:**  
  This dataset was created to support the development of a smart decision-making system for agriculture. It enables predictive modeling of crop yield based on environmental and agricultural inputs.

- **Creators:**  
  The dataset was compiled and processed by an independent data science practitioner as part of a portfolio project. Dataset collected from the following:

- **Source:** [Kaggle Crop Yield Dataset](https://www.kaggle.com/code/patelris/crop-yield-eda-viz/notebook)  
- **Derived From:**  
  - [FAO – Food and Agriculture Organization](http://www.fao.org/home/en/)  
  - [World Bank Open Data](https://data.worldbank.org/)  

> Includes data on crop yield, rainfall, temperature, pesticide usage, crop types, and regions across multiple years.


---

##  Composition

- **Instances Represented:**  
  Each record represents a crop yield observation for a specific crop type, region (country), and year, along with associated environmental and agricultural metrics.

- **Total Records:**  
  13,136 instances

- **Missing Data:**  
  Yes — missing values were present in rainfall data and handled using bootstrap imputation.

- **Confidentiality:**  
  No — the dataset contains no personally identifiable or confidential information.

---

##  Collection Process

- **Data Sources:**  
  The dataset was compiled from four CSV files:
  - `yield.csv`  
  - `rainfall.csv`  
  - `temp.csv`  
  - `pesticides.csv`

- **Acquisition Method:**  
  Data was sourced from publicly available repositories and manually merged.

- **Sampling Strategy:**  
  No sampling was applied; full datasets were used.

- **Time Frame:**  
  Data spans multiple years, with temperature data aligned to start from 1961.

---

##  Preprocessing / Cleaning / Labeling

- **Steps Taken:**  
  - Standardized column names across all datasets  
  - Renamed key columns for consistency  
  - Converted data types (e.g., rainfall to numeric)  
  - Removed duplicates and outliers  
  - Imputed missing rainfall values using bootstrap methods  
  - Aggregated rainfall, temperature, and pesticide data by `area` and `year`  
  - Merged all datasets into a unified DataFrame  
  - Engineered new features: `yield_per_pesticide`, `rainfall_temp_ratio`, `year_group`, and `agro_zone` (via K-Means clustering)  
  - One-hot encoded categorical features  
  - Log-transformed `yield` to reduce skewness

- **Raw Data Retention:**  
  Original CSV files were retained for reference and reproducibility.

---

##  Uses

- **Primary Use Case:**  
  Predicting crop yield using environmental and agricultural inputs.

- **Other Potential Uses:**  
  - Studying environmental impacts on agriculture  
  - Regional crop planning and resource optimization  
  - Climate-based agricultural zoning

- **Risks & Mitigation:**  
  - The dataset does not include socio-economic or soil health data, which may limit its scope.  
  - Users should avoid overgeneralizing results without considering local farming practices.  
  - Interpretations should be contextualized to avoid misinformed policy or investment decisions.

- **Unsuitable Uses:**  
  - Personal or commercial profiling  
  - Applications requiring real-time or hyper-local precision without further validation

---

##  Distribution

- **Distribution Method:**  
  Shared via GitHub as part of a public portfolio project.

- **Licensing & Terms:**  
Data is derived from public sources and shared under open use for educational and research purposes. 

---

##  Related Files & Resources

-  **[Link to Data Preprocessing Code](Part1_MM_25_3_Portfolio_Project.ipynb)**

-  **[Link to Main Model Building Code](Part2_MM_25_3_Portfolio_Project.ipynb)**

-  **[Link to Main Data File](final_crop_yield_data.csv)**

-  **[Link to Read Me File](README.md)**
  

