# Wildfire Smoke Impact and Health Analysis Project

## Overview

This project examines the effects of wildfire smoke on air quality and health outcomes in the United States, with a focus on Jackson, Mississippi. By integrating geospatial wildfire data, air quality indices, and mortality data, the analysis provides insights into both immediate and long-term consequences of wildfire smoke exposure.

The project is divided into two major components:
1. **Wildfire Smoke and Air Quality Analysis**
2. **Wildfire Smoke and Health Outcomes Analysis**

---
## Project Structure
```
   Project/
   │
   ├── data/
   │   ├── Fire_Feature_Data.gdb                 # Geodatabase containing wildfire data
   │   ├── clean_aqi_data.csv                    # Cleaned AQI data with annual pollutant averages
   │   ├── COPD.csv                              # COPD mortality data
   │   ├── heart_diseases.csv                    # Heart disease mortality data
   │   ├── hypertension.csv                      # Hypertension mortality data
   │   ├── lung_cancer.csv                       # Lung cancer mortality data
   │   ├── raw_aqi_data.csv                      # Raw AQI data with bounding box
   │   ├── smoke_impact.csv                      # Annual smoke impact estimates
   │   ├── total.csv                             # All-cause mortality data
   │   ├── weighted_aqi_estimate.csv             # Weighted AQI estimates
   │   └── Wildland_Fire_Polygon_Metadata.xml    # Metadata for wildfire polygon dataset
   │
   │
   ├── output/
   │   ├── viz1.png                              # Histogram of wildfire distances
   │   ├── viz2.png                              # Total acres burned per year
   │   ├── viz3.png                              # Smoke impact and AQI estimates
   │
   ├── src/
   │   ├── initial_analysis.ipynb               # Notebook for smoke impact and air quality analysis
   │   ├── data_exploration.ipynb               # Notebook for health impact analysis
   │   ├── signup.ipynb                         # Auxiliary notebook for data setup
   │
   ├── LICENSE                                   # License information
   ├── README.md                                 # Project overview and setup instructions
   └── .gitignore                                # Git ignore file
```

---

## Data Sources

### 1. **Wildland Fire Data**
- **Source**: U.S. Geological Survey (USGS) Combined Wildland Fire Datasets  
- **Description**: A comprehensive geodatabase covering wildfires and prescribed burns in the United States from 1835 to 2020. This dataset consolidates 40 existing datasets into a unified geospatial dataset with one fire polygon per year for a given area, eliminating duplicate data.  
- **Purpose**: Provides geospatial and temporal wildfire data to estimate smoke impact on nearby regions.  
- **Access**: [USGS Wildland Fire Dataset](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81)  
- **Key File**: `Fire_Feature_Data.gdb`  
- **License**: Public domain under the U.S. Geological Survey's terms of use.  

### 2. **Air Quality Data**
- **Source**: U.S. Environmental Protection Agency (EPA) Air Quality System (AQS)  
- **Description**: Hourly and daily air quality index (AQI) data for pollutants such as PM2.5, PM10, and ozone.  
- **Purpose**: Used to evaluate the relationship between wildfire smoke and changes in air quality, focusing on pollutants most affected by smoke.  
- **Key Files**:
  - `aqi_data.csv`: Contains pollutant levels over time with columns for `Date`, `PM2.5`, `PM10`, `Ozone`, and `AQI`.
  - `clean_aqi_data.csv`: A processed version with annual pollutant averages.  
- **License**: Publicly available via EPA's Open Data Portal.  

### 3. **MSTAHRS Health Data**
- **Source**: Mississippi Statistically Automated Health Resource System (MSTAHRS)  
- **Description**: Health statistics for Hinds County, Mississippi, focusing on annual mortality rates by cause of death. Data are categorized by age group, sex, race, and ethnicity.  
- **Purpose**: Explores correlations between wildfire smoke and health outcomes, with a focus on respiratory and cardiovascular diseases.  
- **Access**: [MSTAHRS Health Data](https://mstahrs.msdh.ms.gov/forms/morttable.html)  
- **Key Files**:
  - `birth_defects.csv`: Annual deaths due to birth defects.
  - `COPD.csv`: Chronic Obstructive Pulmonary Disease mortality rates.
  - `hypertension.csv`: Deaths due to hypertension.
  - `lung_cancer.csv`: Lung cancer mortality rates.
  - `heart_diseases.csv`: Heart disease mortality rates.
  - `total.csv`: Total mortality rates for all causes.  
- **License**: Publicly accessible with no usage restrictions.  

---

## Data Files Description

### **Wildland Fire Data**
- **File**: `Fire_Feature_Data.gdb`  
  - **Type**: Geodatabase  
  - **Attributes**:
    - `Year`: Year of the fire event.
    - `Polygon`: Spatial boundary of the wildfire.
    - `Fire_Type`: Type of fire (wildfire or prescribed burn).
    - `Size`: Area burned (acres).
    - `Tier`: Data quality ranking from 1 (highest) to 8 (lowest).

### **Air Quality Data**
- **File**: `aqi_data.csv`  
  - **Columns**:
    - `Date`: Date of measurement.
    - `PM2.5`: Fine particulate matter concentration (µg/m³).
    - `PM10`: Coarse particulate matter concentration (µg/m³).
    - `Ozone`: Ozone concentration (ppm).
    - `AQI`: Air Quality Index value.

- **File**: `clean_aqi_data.csv`  
  - **Columns**:
    - `Year`: Year of measurement.
    - `Avg_PM2.5`: Annual average of PM2.5.
    - `Avg_PM10`: Annual average of PM10.
    - `Avg_Ozone`: Annual average of Ozone.
    - `Annual_AQI`: Annual AQI value.

### **Health Data**
Each file (`birth_defects.csv`, `COPD.csv`, `hypertension.csv`, etc.) has the same structure:  
- **Columns**:
  - `Year`: Year of mortality data.
  - `Number`: Total number of deaths for the category in that year.

---

## Methodology

### **Part 1: Wildfire Smoke and Air Quality**
1. **Data Cleaning and Processing**:
   - Geospatial fire polygons were filtered by proximity to urban areas.
   - AQI data were processed to calculate annual averages.
   
2. **Smoke Impact Estimate**:
   - Calculated using a formula incorporating fire size, distance to urban centers, and pollutant levels from AQI.

3. **Exploratory Data Analysis**:
   - Visualized trends in wildfire occurrence and AQI changes over time.
   - Mapped spatial distribution of fire events using `geopandas`.

4. **Forecasting**:
   - Applied statistical models (ARIMA, Prophet) to predict future AQI trends based on historical smoke impact.

### **Part 2: Wildfire Smoke and Health Outcomes**
1. **Data Integration**:
   - Combined smoke impact estimates with health data (e.g., `COPD.csv`, `heart_diseases.csv`).

2. **Lagged Analysis**:
   - Introduced a five-year lag to explore long-term health impacts of smoke exposure.

3. **Statistical Analysis**:
   - Correlation analysis between wildfire smoke estimates and mortality rates.
   - Regression models to determine the strength of associations.

4. **Visualization**:
   - Created heatmaps, scatterplots, and trendlines to illustrate relationships.
   - Highlighted specific years with significant health and AQI changes.

---

## Outputs

- **Visualizations**:
  - `viz1.png`: Histogram of wildfire distances to urban centers.
  - `viz2.png`: Yearly acreage burned.
  - `viz3.png`: Smoke impact vs. AQI trends.

- **Processed Data**:
  - `weighted_aqi_estimate.csv`: Smoke impact metrics.
  - `smoke_impact.csv`: Annual smoke exposure estimates.

---

## Insights and Findings

### Wildfire Smoke and Air Quality
- **Strong positive correlation** between wildfire smoke and AQI metrics, especially PM2.5.
- Predictive models indicate **increasing smoke impact** due to climate change.

### Wildfire Smoke and Health Outcomes
- Significant correlations observed between smoke impact and:
  - **COPD mortality rates** (immediate impact).
  - **Hypertension and lung cancer** (lagged impact).
- Long-term exposure to wildfire smoke poses **serious public health risks**.

---

## Installation and Usage

### Prerequisites
- Python 3.7+
- Required Libraries: `pandas`, `numpy`, `matplotlib`, `seaborn`, `geopandas`, `statsmodels`, `scipy`, `fiona`.

### Setup
1. Clone the repository:
   ```bash
   git clone https://github.com/c0zimb4tm4n/wildland-fire-predictive-analysis.git
   cd wildfire-health-analysis
   ```
2. Install dependecies:
   ```bash
   pip install -r requirements.txt
   ```
3. Configure API keys (e.g., EPA AQS) in initial_analysis.ipynb and data_exploration.ipynb.

### Running the Analysis
- Part 1: Run initial_analysis.ipynb to analyze wildfire smoke and air quality data.
- Part 2: Run data_exploration.ipynb to study health outcomes.


## License and Acknowledgments

This project is licensed under the **MIT License**.

### Data Sources
- **Wildland Fire Data**: [USGS Wildland Fire Dataset](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81)
- **Air Quality Data**: [EPA's Air Quality System](https://www.epa.gov/aqs)
- **Health Data**: [MSTAHRS](https://mstahrs.msdh.ms.gov/forms/morttable.html)

### Acknowledgments
We thank the **USGS Wildland Fire Advisory Group** and **MSTAHRS** for making these datasets available for research and educational purposes.

