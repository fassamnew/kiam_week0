# kiam_week0
This project tries to address the problem MoonLight Energy Solutions is facing regarding their solar panel deployment project. 

**MoonLight Energy** Solutions aims to develop a strategic approach to significantly enhance its operational efficiency and sustainability through targeted solar investments. As an Analytics Engineer at MoonLight Energy Solutions, your task is to perform a quick analysis of an environmental measurement provided by the engineering team and translate your observation as a strategy report. Your analysis should focus on identifying key trends and learn valuable insights that will support your data-driven case - your recommendation based on the statistical analysis and EDA.  In particular, your analysis and recommendation must present a strategy focusing on identifying high-potential regions for solar installation that align with the company's long-term sustainability goals. Your report should provide an insight to help realize the overarching objectives of MoonLight Energy Solutions.

Solar Radiation Measurement Data
The data for this week's challenge is extracted and aggregated from Solar Radiation Measurement Data. Each row in the data contains the values for solar radiation, air temperature, relative humidity, barometric pressure, precipitation, wind speed, and wind direction, cleaned and soiled radiance sensor (soiling measurement) and cleaning events.

The structure of the data is as follows

-**Timestamp (yyyy-mm-dd hh:mm)**: Date and time of each observation.
-**GHI (W/m²)**: Global Horizontal Irradiance, the total solar radiation received per square meter on a horizontal surface.
-**DNI (W/m²)**: Direct Normal Irradiance, the amount of solar radiation received per square meter on a surface perpendicular to the rays of the sun.
-**DHI (W/m²)**: Diffuse Horizontal Irradiance, solar radiation received per square meter on a horizontal surface that does not arrive on a direct path from the sun.
-**ModA (W/m²)**: Measurements from a module or sensor (A), similar to irradiance.
-**ModB (W/m²)**: Measurements from a module or sensor (B), similar to irradiance.
-**Tamb (°C)**: Ambient Temperature in degrees Celsius.
-**RH (%)**: Relative Humidity as a percentage of moisture in the air.
-**WS (m/s)**: Wind Speed in meters per second.
-**WSgust (m/s)**: Maximum Wind Gust Speed in meters per second.
-**WSstdev (m/s)**: Standard Deviation of Wind Speed, indicating variability.
-**WD (°N (to east))**: Wind Direction in degrees from north.
-**WDstdev**: Standard Deviation of Wind Direction, showing directional variability.
-**BP (hPa)**: Barometric Pressure in hectopascals.
-**Cleaning (1 or 0)**: Signifying whether cleaning (possibly of the modules or sensors) occurred.
-**Precipitation (mm/min)**: Precipitation rate measured in millimeters per minute.
-**TModA (°C)**: Temperature of Module A in degrees Celsius.
-**TModB (°C)**: Temperature of Module B in degrees Celsius.
-**Comments**: This column is designed for any additional notes.