## Data Collection and Processing Overview

This notebook outlines the steps taken to collect and process agricultural and climate-related data for crop yield analysis.

### 📥 Data Collection

The data was sourced from four separate CSV files:

- [📋 Link to yield Data File](yield.csv)
- [📋 Link to yield Data File](rainfall.csv)
- [📋 Link to yield Data File](temp.csv)
- [📋 Link to yield Data File](pesticides.csv)

- [📋 Link to Main Data File after data pre processing](final_crop_yield_data.csv)

Each file represents a different aspect of the dataset: crop yield, rainfall patterns, temperature records, and pesticide usage.

---

### ⚙️ Data Processing Steps

1. **Previewing and Inspecting Datasets**  
   - Used `.head()` and `.describe()` to examine the structure and basic statistics of each DataFrame.

2. **Dropping Unwanted Columns**  
   - Removed irrelevant columns from `total_crop_data` and `pesticides_data` to streamline analysis.

3. **Standardizing Column Names**  
   - Applied a function to strip whitespace, convert to lowercase, and replace spaces with underscores across all DataFrames.

4. **Renaming Columns for Consistency**  
   - Renamed:
     - `'value'` → `'yield'` in `total_crop_data`
     - `'country'` → `'area'` in `temperature_data`
     - `'value'` → `'pesticides_tonnes'` in `pesticides_data`

5. **Checking and Fixing Data Types**  
   - Converted `average_rain_fall_mm_per_year` in `rainfall_data` from object to numeric using `pd.to_numeric(errors='coerce')`.

6. **Aligning Year Range**  
   - Filtered out rows in `temperature_data` with years before 1961 to match the time frame of `total_crop_data`.

7. **Handling Duplicates**  
   - Checked for duplicates in all datasets and removed them from `temperature_data`.

8. **Handling Missing Values**  
   - Identified missing values across datasets.
   - Applied **bootstrap imputation** to fill missing values in `average_rain_fall_mm_per_year` in `rainfall_data`.

9. **Outlier Detection and Handling**  
   - Visualized and assessed outliers in all datasets.
   - Retained genuine outliers in pesticide data.
   - Removed a single extreme outlier in `total_crop_data`.

10. **Aggregating Data**  
    - Aggregated `rainfall`, `temperature`, and `pesticides` data by `'area'` and `'year'`, computing the mean for each group.

11. **Merging Datasets**  
    - Merged the aggregated datasets with `total_crop_data` using `'area'` and `'year'` as keys.

12. **Saving the Final Dataset**  
    - Saved the merged DataFrame in both `.csv` and `.pkl` formats for future use.

---
## 📊 Additional Resources

- [📋 Link To ReadMe File](ReadMe.md) 
- [📈 Link to Main Model Building Code](Part2_MM_25_3_Portfolio_Project.ipynb)  
- [📋 Model Card](model_card.md)  
- [📄 Data Sheet](data_sheet.md)
- [📈 Link to overview of Main Model](Overview_Of_Main_Model_Flow.md) 
- [📈 Link to overview of Data Preprocessing](Overview_Of_Data__Pre-Processing.md)
- [📈 Link to Data Pre-Processing Code](Part1_MM_25_3_Portfolio_Project.ipynb) 
- [📋 Link to Main Data File](final_crop_yield_data.csv)

### ✅ Final Output

The result is a clean, merged dataset containing:

- Crop yield
- Rainfall
- Temperature
- Pesticide usage

This dataset is now ready for further analysis and model 