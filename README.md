True Prosperity Index (TPI) – CA & NY Counties

Final Data Science Bootcamp Project

📌 Overview

This project creates a county-level socioeconomic dataset for California and New York, combining median household income, poverty rate, unemployment rate, and life expectancy. These indicators support building a True Prosperity Index (TPI), conducting clustering analyses, running regression models, and generating geospatial visualizations.

The dataset is built entirely from publicly available sources: American Community Survey (ACS) 2022 and County Health Rankings (CHR) 2024/2025.

🎯 Goal

The goal is to understand local wellbeing in a way that reflects people’s lived experiences, not just economic indicators like GDP or the stock market. Cities and communities require ground-level data to reveal patterns in prosperity and identify areas needing intervention.

📂 Repository Structure

├── data/
│   ├── county_data_final.csv       # The cleaned, merged dataset used for analysis
│   └── cb_2018_us_county_500k/     # Shapefiles for US Census tracts/counties (for GeoPandas)
│
├── notebooks/
│   └── Final_Project_Notebook.ipynb # Main analysis code (TPI construction, Clustering, Regression)
│
├── presentation/
│   ├── TPI_Project_Presentation.pptx
│   └── TPI_Project_Presentation.pdf
│
└── README.md


📊 Data Sources

American Community Survey (ACS 2022)

S1901: Income (Median household income)

S1701: Poverty (Percent below poverty)

S2301: Employment (Unemployment rate)

County Health Rankings (2024/2025)

Life expectancy by county

FRED (Federal Reserve Economic Data)

S&P 500 Daily Values (used for market vs. community comparison)

🛠 Step-by-Step Dataset Creation

1. Collecting ACS Data

ACS Subject Tables (S1901, S1701, S2301) were downloaded for all counties in CA and NY. These tables were originally in wide-format.

Issue: Each county was a column, not a row.

Solution: Custom extraction functions were written to:

Identify the correct indicator row (e.g., “Median income (dollars)”).

Select columns ending in “!!Estimate”.

Split the county and state from the column names.

Standardize the output format.

2. Cleaning & Standardizing County Names

Issue: County names varied across sources (e.g., “Los Angeles County, California” vs “Los Angeles”).

Solution: Removed state suffixes, ensured consistent "County" suffix, and standardized naming conventions.

3. Adding State Abbreviations

Mapped "California" → "CA" and "New York" → "NY" to assist in merging and mapping.

4. Collecting Life Expectancy (CHR)

Downloaded CA and NY life expectancy CSV files from the County Health Rankings website.

Issue: Column names did not match expected values (used “County Value**”).

Solution: Renamed “County Value**” to life_expectancy.

Issue: Some counties lacked the "County" suffix.

Solution: Standardized naming by appending “County” consistently.

5. Merging All Data Sources

Merged ACS income, poverty, and unemployment data with life expectancy using county_name + state_abbr. Cleaned numeric fields by removing commas and percentage signs.

📝 Final Dataset Output

The processed file (county_data_final.csv) contains the following columns:

Column Name

Description

county_name

Name of the county (e.g., "Alameda County")

state_abbr

State abbreviation (CA or NY)

median_income

Median Household Income ($)

poverty_rate

Percentage of population below poverty line (%)

unemployment_rate

Unemployment rate (%)

life_expectancy

Average life expectancy in years

🚀 Usage & Analysis

The Jupyter Notebook (Final_Project_Notebook.ipynb) performs the following:

Standardization: Converts all metrics to Z-scores.

TPI Construction: Calculates the composite index (0-100 scale).

Clustering: Uses K-Means to identify Low, Moderate, and High prosperity tiers.

Modeling: Uses Logistic Regression to identify drivers of prosperity.

Visualization: Compares TPI against S&P 500 data and maps regional trends.

Requirements

To run the notebook, ensure you have the following Python libraries installed:

pip install pandas numpy matplotlib seaborn scikit-learn geopandas
