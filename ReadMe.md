# 🌦 East Africa Temperature Dashboard — Power BI + OpenWeatherMap API

## 🧩 Problem Statement

Accessing up-to-date and reliable weather information across East African cities can be fragmented and inconsistent across multiple sources.  
This project aims to centralize real-time weather data by connecting **Power BI** directly to the **OpenWeatherMap API** to monitor **temperature**, **humidity**, and **pressure** across key cities — **Nairobi, Mombasa, Kampala, and Kigali**.  

The objective was to:
- Build a **live, automated dashboard** that retrieves and visualizes weather data from an API.
- Demonstrate how to **connect REST APIs to Power BI** using **Power Query (M language)**.
- Create an **interactive experience** that allows users to compare and explore weather metrics across cities in real time.

---

## 🛠 Methods & Tools

### Tools Used
| Tool / Service | Purpose |
|----------------|----------|
| **Power BI Desktop** | Data visualization, dashboard creation |
| **Power Query (M language)** | API connection, data transformation, and JSON parsing |
| **OpenWeatherMap API** | Source of live weather data |
| **DAX (Data Analysis Expressions)** | Measures and interactivity logic |
| **GitHub** | Version control and project documentation |

### Methodology

#### 1. Data Source
- API Endpoint:  
  ```
  https://api.openweathermap.org/data/2.5/weather?q={city}&appid={API_KEY}
  ```
- Data Fields Extracted:
  - `main.temp` → Temperature (Kelvin → converted to °C)
  - `main.humidity` → Humidity (%)
  - `main.pressure` → Pressure (hPa)
  - `name` → City name

#### 2. Data Acquisition (Power Query Function)
A reusable **Power Query function** was created to dynamically call the API for multiple cities.


The function is then invoked dynamically on a **Cities table**:
| City     |
|-----------|
| Nairobi   |
| Mombasa   |
| Kampala   |
| Kigali    |

---

### 3. Data Transformation
- Expanded and cleaned API response fields
- Converted temperature from **Kelvin to Celsius**
- Changed data types to numeric (Decimal & Whole Number)
- Created calculated DAX measures for aggregation and interactivity

### 4. Measures Created (DAX)
```DAX
AvgTemperature_C = AVERAGE(Cities[Temperature_C])
AvgHumidity = AVERAGE(Cities[Humidity])
AvgPressure = AVERAGE(Cities[Pressure])

SelectedTemp_C = SELECTEDVALUE(Cities[Temperature_C], [AvgTemperature_C])
SelectedHumidity = SELECTEDVALUE(Cities[Humidity], [AvgHumidity])
SelectedPressure = SELECTEDVALUE(Cities[Pressure], [AvgPressure])
```

These measures drive **card visuals**, **bar charts**, and **tooltips** dynamically.

---

## 📊 Results & Key Takeaways

### 🧠 Insights
- **Mombasa** consistently records the **highest temperature** among the four cities.  
- **Kigali** and **Kampala** display cooler and more humid conditions, typical of their elevation.  
- Real-time integration with APIs enables **up-to-date reporting** without manual data entry.

### 💡 Key Dashboard Features
| Feature | Description |
|----------|--------------|
| 🌍 **City Slicer** | Allows filtering of all visuals dynamically |
| 🌡 **Interactive Cards** | Display temperature, humidity, and pressure in real time |
| 📊 **Bar Chart Comparison** | Visual comparison of temperature across cities |
| 🧭 **Drillthrough Page** | Right-click a city → open detailed breakdown |
| 🪶 **Tooltip Page** | Hover over a city → quick metrics popup |
| 🔁 **Automatic Refresh** | Data refreshes via API upon Power BI refresh |
| 🔐 **Parameterized API Key** | Securely stored key using Power Query parameters |

---



## 📈 Dashboard Preview

![Dashboard Screenshot]([assets/dashboard_preview.png](https://github.com/Wakaba2024/OpenWeather_BI_Dashboard-/blob/main/Screenshot%202025-11-11%20101809.png))

**Dashboard Layout**
- Title: *East Africa Temperature Dashboard*
- Top Cards: Temperature (°C), Humidity (%), Pressure (hPa)
- Bar Chart: Temperature by City
- Filters: City Slicer
- Drillthrough Page: City Details

---

## 🧩 Challenges Faced
1. Handling **API rate limits** during multiple data refreshes.  


---

## 🧠 Lessons Learned
- **Power Query functions** are essential for scalable API integrations.  
- Using `try ... otherwise` prevents data refresh failures.  
- **SELECTEDVALUE()** in DAX adds powerful context-awareness to visuals.  
- Parameterizing the API key enhances **security and reusability**.  
- Combining tooltips, slicers, and drillthroughs creates a **professional, interactive experience**.

---

## 🚀 Future Improvements
- Add more cities across East Africa dynamically.  
- Include **5-day forecasts** using the OpenWeatherMap `/forecast` endpoint.  
- Integrate **Air Quality Index (AQI)** data for environmental insights.  



---

## 🪪 License
This project is licensed under the **MIT License** — you are free to use, modify, and share with attribution.

---


