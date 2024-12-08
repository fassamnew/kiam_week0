# Data Analysis and Cleaning for Solar Radiation and Meteorological Data

In this project, I explored and cleaned a dataset containing solar radiation and meteorological measurements over time. The goal was to analyze patterns in solar irradiance, temperature, and wind conditions while ensuring that the dataset was clean, complete, and free of anomalies for further analysis. Below is a summary of the tasks I accomplished, from initial data loading to advanced analysis.

## 1. **Data Loading and Exploration**

I started by loading the dataset containing various solar and meteorological measurements. The dataset includes columns such as Global Horizontal Irradiance (GHI), Direct Normal Irradiance (DNI), Diffuse Horizontal Irradiance (DHI), ambient temperature (Tamb), wind speed, and more.

### Steps:
- I loaded the dataset using `pandas.read_csv()`, specifying the correct file path for each dataset.
- I performed initial checks to ensure that the data was loaded correctly, and printed out the first few rows of the dataset.

```python
import pandas as pd

# Filepath of the CSV data
file_path = "../../data/benin-malanville.csv"  # Change this as needed

# Load the data
data = pd.read_csv(file_path, parse_dates=["Timestamp"])
```
## 2. **Data Quality Check**
After loading the data, I conducted an initial data quality check. This involved identifying missing values, checking for duplicate rows, and inspecting the data types of each column. I also identified any columns that had entirely missing values, such as the Comments column, and flagged any issues that might require further cleaning.

Key Actions:
Removed columns with entirely missing values (e.g., Comments).
Identified missing values in numerical columns and decided to fill them with the median of each column.
Removed duplicate rows.
```python
# Remove columns with entirely missing values
data.dropna(axis=1, how='all', inplace=True)

# Fill missing values in numerical columns with the median
numerical_columns = ['GHI (W/m²)', 'DNI (W/m²)', 'DHI (W/m²)', 'ModA (W/m²)', 'ModB (W/m²)', 
                     'Tamb (°C)', 'RH (%)', 'WS (m/s)', 'WSgust (m/s)', 'WSstdev (m/s)', 
                     'WD (°N (to east))', 'BP (hPa)', 'Precipitation (mm/min)', 
                     'TModA (°C)', 'TModB (°C)']
data[numerical_columns] = data[numerical_columns].fillna(data[numerical_columns].median())
```
## 3. **Time Series Analysis and Visualization**
I explored the relationships betIen solar irradiance, temperature, and other meteorological variables over time. This helped us observe trends, seasonal patterns, and anomalies.

Key Visualizations:
Line charts Ire used to plot the changes in GHI, DNI, DHI, and Tamb over time.
I aggregated the data by month to identify any seasonal patterns.
I plotted the trends throughout the day for key variables.

```python

import matplotlib.pyplot as plt

# Example: Plotting GHI over time
plt.figure(figsize=(10, 6))
plt.plot(data['Timestamp'], data['GHI (W/m²)'], label='GHI')
plt.xlabel('Timestamp')
plt.ylabel('Global Horizontal Irradiance (W/m²)')
plt.title('Global Horizontal Irradiance Over Time')
plt.legend()
plt.show()
```
## 4. **Correlation Analysis**
To better understand the relationships betIen different variables, I performed correlation analysis. I used correlation matrices and pair plots to visualize how solar irradiance components (GHI, DNI, DHI) correlated with temperature measurements (TModA, TModB) and other meteorological conditions.

Insights:
I discovered strong correlations betIen GHI, DNI, and DHI, which are expected given their similar physical nature.
I also explored how wind conditions (e.g., wind speed, gust speed) relate to solar irradiance.
```python
import seaborn as sns

# Correlation matrix for solar radiation and temperature
correlation_data = data[['GHI (W/m²)', 'DNI (W/m²)', 'DHI (W/m²)', 'TModA (°C)', 'TModB (°C)']]
sns.heatmap(correlation_data.corr(), annot=True, cmap="coolwarm", linewidths=0.5)
plt.title('Correlation Matrix of Solar Radiation and Temperature')
plt.show()
```
## 5. **Wind Analysis**
I also examined the wind data, which included variables like wind speed (WS), gust speed (WSgust), and wind direction (WD). To visualize wind trends, I used wind rose diagrams to show the distribution of wind speed and direction, as well as how variable the wind direction tends to be.

```python
# Wind rose visualization
from windrose import WindroseAxes

# Plotting wind direction and speed
ax = WindroseAxes.from_ax()
ax.bar(data['WD (°N (to east))'], data['WS (m/s)'], bins=12, normed=True, opening=0.8, edgecolor='white')
ax.set_title('Wind Rose for Wind Speed and Direction')
plt.show()
```
## 6. **Handling Missing Data and Anomalies**
During my analysis, I observed a potential for few issues with the data, such as negative values in the GHI, DNI, and Tamb columns, which are physically impossible. I addressed these anomalies by replacing the negative values with NaN and then filled those missing values with the median for each column.

Anomaly Handling Code:
```python
def handle_anomalies(df):
    # Replace negative values in specific columns with NaN
    columns_with_anomalies = ['GHI (W/m²)', 'DNI (W/m²)', 'DHI (W/m²)', 'ModA (W/m²)', 'ModB (W/m²)', 
                              'Tamb (°C)', 'TModA (°C)', 'TModB (°C)']
    for col in columns_with_anomalies:
        df.loc[df[col] < 0, col] = pd.NA  # Replace negative values with NaN
    
    # Fill NaN values with the median
    df[columns_with_anomalies] = df[columns_with_anomalies].fillna(df[columns_with_anomalies].median())

    return df

data = handle_anomalies(data)
```
## 7. **Saving Cleaned Data**
Finally, after performing all necessary cleaning and handling anomalies, I saved the cleaned data into a new CSV file, which is now ready for further analysis or machine learning applications.

```python
# Save the cleaned data for further analysis
cleaned_file_path = "../../data/cleaned_benin_malanville.csv"
data.to_csv(cleaned_file_path, index=False)
print(f"Cleaned data saved to {cleaned_file_path}.")
```
## **Conclusion**
This project involved several steps in cleaning and analyzing solar radiation and meteorological data. I started by loading and exploring the dataset, then proceeded to clean the data by handling missing values and anomalies. Through visualization and statistical analysis, I explored trends in solar irradiance, temperature, and wind conditions over time. I also visualized the relationships betIen variables like solar radiation, temperature, and wind, providing valuable insights into the data's behavior.

This analysis can be extended further to build predictive models, understand seasonal patterns, or assess the impact of Iather conditions on solar energy production.