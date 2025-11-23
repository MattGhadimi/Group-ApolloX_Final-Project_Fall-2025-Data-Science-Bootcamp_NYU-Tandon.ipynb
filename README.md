# True Prosperity Index (TPI) – CA & NY Counties  
### Final Data Science Bootcamp Project

---

## 📌 Overview  
This project creates a county-level socioeconomic dataset for California and New York, combining:  
- Median household income  
- Poverty rate  
- Unemployment rate  
- Life expectancy  

These indicators support:  
- Constructing a **True Prosperity Index (TPI)**  
- Performing **clustering** (Low / Moderate / High Prosperity)  
- Running **regression models**  
- Building **geospatial visualizations**  

All data is sourced from publicly available datasets:  
- **American Community Survey (ACS) 2022**  
- **County Health Rankings (CHR) 2024/2025**

---

## 🎯 Goal  
The goal is to measure local wellbeing in a way that reflects people’s lived experiences—not just macroeconomic indicators like GDP or the stock market.  
The dataset enables deeper understanding of prosperity patterns and helps identify regions needing intervention.

---

## 📂 Repository Structure  

├── data/
│ ├── county_data_final.csv # Cleaned, merged dataset
│ └── cb_2018_us_county_500k/ # U.S. Census shapefiles (for GeoPandas)
│
├── notebooks/
│ └── Final_Project_Notebook.ipynb # Full analysis: TPI, Clustering, Regression
│
├── presentation/
│ ├── TPI_Project_Presentation.pptx
│ └── TPI_Project_Presentation.pdf
│
└── README.md


---

## 📊 Data Sources  

### **American Community Survey (ACS 2022)**  
- `S1901` – Median household income  
- `S1701` – Percent below poverty  
- `S2301` – Unemployment rate  

### **County Health Rankings (CHR 2024/2025)**  
- Life Expectancy by County  

### **Federal Reserve Economic Data (FRED)**  
- S&P 500 Daily Values  
  *(Used to compare market volatility vs. stability of community prosperity)*  

---

## 🛠 Step-by-Step Dataset Creation  

### **1. Collecting ACS Data**  
ACS subject tables (S1901, S1701, S2301) were downloaded for CA and NY.  

**Issue:**  
ACS tables were in **wide format** (each county = a column).  

**Solution:**  
Custom Python functions were written to:  
- Identify the correct value rows (e.g., *“Median income (dollars)”*)  
- Select columns ending in `!!Estimate`  
- Parse county/state names from column headers  
- Standardize output into tidy tabular format  

---

### **2. Cleaning & Standardizing County Names**  
**Issue:**  
County names differed across sources (e.g., *“Los Angeles County, California”*, *“Los Angeles”*).  

**Solution:**  
- Removed state suffixes  
- Ensured consistent `"County"` suffix  
- Standardized naming conventions across all datasets  

---

### **3. Adding State Abbreviations**  
Mapped state names into two-letter abbreviations:  
- California → **CA**  
- New York → **NY**  

---

### **4. Collecting Life Expectancy (CHR)**  
Life expectancy CSVs were downloaded for CA and NY.  

**Issue:**  
Column name was `"County Value**"` instead of expected `"life_expectancy"`.  

**Solution:**  
- Renamed `"County Value**"` → `life_expectancy`  
- Ensured all counties had a consistent `"County"` suffix  

---

### **5. Merging All Data Sources**  
Merged ACS income, poverty, and unemployment with CHR life expectancy using:  



Numeric data was cleaned by removing:  
- Commas from income values  
- Percentage signs from poverty/unemployment indicators  

---

## 📝 Final Dataset Output  

The processed file `county_data_final.csv` contains:

| Column Name         | Description                                           |
|---------------------|-------------------------------------------------------|
| `county_name`       | County name (e.g., "Alameda County")                  |
| `state_abbr`        | State abbreviation (`CA` or `NY`)                     |
| `median_income`     | Median Household Income (USD)                         |
| `poverty_rate`      | Percent below poverty (%)                             |
| `unemployment_rate` | Unemployment rate (%)                                 |
| `life_expectancy`   | Average life expectancy (years)                       |

---

## 🚀 Usage & Analysis  

The notebook `Final_Project_Notebook.ipynb` performs:

### **✔ Standardization**  
Converts all raw metrics into Z-scores for comparability.

### **✔ TPI Construction**  
Builds the composite True Prosperity Index (scaled 0–100).

### **✔ Clustering**  
Uses K-Means to assign each county into:  
- **Low Prosperity**  
- **Moderate Prosperity**  
- **High Prosperity**

### **✔ Modeling**  
Logistic Regression identifies which indicators most strongly predict high prosperity.

### **✔ Visualization**  
- TPI distribution  
- Prosperity tiers  
- Logistic regression coefficients  
- S&P 500 vs. TPI stability  
- Geospatial maps using U.S. Census shapefiles  

---

## 📦 Requirements  

Install all dependencies using:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn geopandas
