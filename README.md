# Real-Time Weather Forecasting & Analytics Dashboard 🌦️

## Project Overview
This project is an automated, interactive meteorological tracking system built in Microsoft Power BI. Instead of relying on static historical datasets, it utilizes a custom mini-ETL pipeline to pull live 7-day forecasts and current environmental conditions from a RESTful Weather API. 

The dashboard provides real-time, data-driven insights into temperature trends, Air Quality Indices (AQI), atmospheric pressure, and humidity for six distinct cities in Maharashtra (Chhatrapati Sambhajinagar, Nanded, Jalna, Mumbai, Nagpur, and Pune).

## 🛠️ Tech Stack & Tools
* **Business Intelligence:** Microsoft Power BI Desktop
* **Data Transformation (ETL):** Power Query (M Language)
* **Calculations & Measures:** DAX (Data Analysis Expressions)
* **Data Source:** WeatherAPI.com (RESTful Web API, JSON format)

## ⚙️ The Data Engineering Pipeline
A significant focus of this project was engineering a robust data pipeline to handle dynamic, hierarchical JSON payloads.

1. **API Integration & Parsing:** Established web connections to fetch rolling 7-day data. Raw nested JSON arrays were expanded and flattened into a tabular `Master_Table`.
2. **Schema Structuring:** To optimize the data model, three specialized tables were derived from the master dataset:
   * `Current_Data`: Isolated real-time weather metrics.
   * `Forecast_Day`: Aggregated daily forecast predictions.
   * `Forecast_Hour`: Granular, hourly meteorological predictions.
3. **Data Modeling:** Designed a robust Star-Schema semantic model establishing 1-to-Many relationships with bi-directional cross-filtering to ensure synchronous visualization updates across geographic slicers.

## 📊 Key Visualizations & DAX Implementation
* **Trend Analysis:** Line charts mapping the 7-day temperature trajectory to highlight warming/cooling curves.
* **Environmental Health:** Donut charts breaking down AQI into specific pollutant levels (PM10, O3, SO2) categorized by dynamic health bands.
* **Real-time KPIs:** Custom cards displaying instantaneous readings for Humidity, Wind Speed, and Atmospheric Pressure.

To keep the semantic model organized, all calculations were isolated into a dedicated `_Measures` table housing 17 custom DAX metrics.

> **Example DAX Measure (Dynamic AQI Status):**
> ```dax
> AQI Status Text = 
> Var AQI = ROUND(SELECTEDVALUE(Current_data[current.air_quality.pm10]),0)
> RETURN
> SWITCH(
>     TRUE(),
>     AQI <= 50, "Good",
>     AQI <= 100, "Moderate",
>     AQI <= 150, "Unhealthy For Sensitivity",
>     AQI <= 200, "Unhealthy",
>     AQI <= 300, "Very Unhealthy",
>     "Hazardous"
> )
> ```

## 📁 Repository Contents
* `Weather_Dashboard.pbix` - The complete Power BI project file (requires Power BI Desktop to view).
* `Dataset/` - Contains a sample dataset (JSON/CSV) demonstrating the raw API payload structure before ETL transformations.
* `Documentation/` - Contains the full project methodology report (`DVTT Mini Project Report.pdf`) and technical architecture diagrams.
* `Images/Screenshots/` - High-resolution captures of the dashboard interface, Power Query workflows, and data modeling.
* `Images/Icons/` - Custom UI assets and symbology implemented within the dashboard.

## 👤 Author
**Vijay Nagargoje** Third-Year B.Tech Student in Artificial Intelligence & Data Science | MIT CSN
