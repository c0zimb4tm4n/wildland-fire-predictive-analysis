# Wildfire Smoke Impact Analysis on Air Quality

## Project Overview
This project aims to analyze the impact of wildfire smoke on air quality for a specific U.S. city, using geospatial wildfire data and air quality index (AQI) data. By developing a quantitative "smoke impact" estimate, the project seeks to inform policy makers and city managers about potential wildfire-related air quality issues.

## Project Structure

- **data/**  
  - Contains the raw and processed data files used for analysis.
    - `Fire_Feature_Data.gdb`: Geodatabase file containing wildfire data.
    - `aqi_data.csv`: Raw AQI data.
    - `clean_aqi_data.csv`: Cleaned AQI data with annual averages for pollutants.
    - `weighted_aqi_estimate.csv`: AQI data with weighted estimates per pollutant.
    - `Wildland_Fire_Polygon_Metadata.xml`: Metadata for wildfire polygons.
  
- **output/**  
  - Stores output visualizations:
    - `viz1.png`: Histogram of wildfire distances.
    - `viz2.png`: Total acres burned per year.
    - `viz3.png`: Smoke impact and AQI estimates over time.
  
- **src/**  
  - Contains Jupyter notebooks for analysis:
    - `initial_analysis.ipynb`: Primary notebook for conducting analyses.
    - `signup.ipynb`: Auxiliary notebook for data setup.

- **.gitignore**  
  - Specifies files and directories to be ignored by Git.

- **LICENSE**  
  - Project license information.

## Methodology

### Part 1: Common Analysis

#### Step 0: Data Acquisition
Wildfire data was obtained from the [US Geological Survey](https://usgs.gov) as polygon shapefiles in a geodatabase format, which included location and size attributes of each fire. AQI data was retrieved via the US EPA's [AQS API](https://aqs.epa.gov).

#### Step 1: Smoke Impact Estimate
For each year from 1961-2021:
1. **Filter Fires by Distance**  
   - Only fires within a 650-mile radius of the assigned city were considered.

2. **Calculate Smoke Impact**  
   - Smoke impact was estimated using fire size (acres), distance from city, and type-based weighting. 

3. **Compare with AQI Data**  
   - A weighted AQI estimate was computed for each year based on pollutant concentrations. 

4. **Predictive Modeling**  
   - Forecast smoke impact for 2025-2050 using ARIMA and Prophet models.

### Visualizations

1. **Histogram of Wildfire Distances**  
   - Distribution of wildfire distances from the city, with a modeling distance cut-off at 650 miles.

2. **Total Acres Burned Per Year**  
   - Time-series plot of total acres burned within the 650-mile radius.

3. **Smoke Impact and AQI Estimates**  
   - Comparative plot of annual smoke impact and AQI estimates.

### Part 2: Extension
To be completed in the next project phase.

## Installation

### Prerequisites
- Python 3.7+
- Packages: `pandas`, `geopandas`, `matplotlib`, `fiona`, `requests`, `prophet`, `statsmodels`, and `geopy`.

### Setup
1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/projectname.git
   cd projectname
   ```
2. Install dependencies:
   ```bash
    pip install -r requirements.txt
   ```

### API Access
Request an API key from the US EPA’s AQS API. Update your USERNAME and APIKEY in the scripts.

### Usage
Run the Jupyter notebooks in src/ for data analysis:
  - initial_analysis.ipynb: Main analysis, data visualization, and forecasting.

### License
MIT License
