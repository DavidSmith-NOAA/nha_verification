Sure! Here’s a **README** that you can copy and paste into a text file. It explains the script's purpose, dependencies, usage, and output details.

---

# **RFC Flood History Extraction Script**  

### **Author:** Charlie Smith  
### **Date:** March 2024  
### **Description:**  
This script extracts flood history data for USGS river gauge sites from the **National Water Prediction Service (NWPS)** and **USGS NWIS** websites. It retrieves river stage data, identifies the highest recorded flood stage, and categorizes it into **action, minor, moderate, or major flood status**. The output includes a **CSV file** and a **map visualization**.

---

## **🔧 Requirements & Dependencies**  

This script requires Python 3.x and the following libraries:  

- `pandas` (for data processing)  
- `numpy` (for numerical operations)  
- `concurrent.futures` (for parallel processing)  
- `urllib.request` (for downloading files)  
- `geopandas` (for spatial data processing)  
- `shapely` (for working with geometric points)  
- `matplotlib` (for visualization)  

### **Installation**  
If you don’t have the required packages installed, use the following command:  
```bash
pip install pandas numpy geopandas shapely matplotlib
```

---

## **📌 How to Use**  

### **1️⃣ Run the Script**  
Run:  
```
NHA_verification.IPYNB in Jupyter Notebooks
```

### **2️⃣ Inputs**  
- The script pulls data for a defined **date range**:
  ```python
  flood_history_begin_date = '2024-03-21'
  flood_history_end_date = '2024-06-30'
  ```
- It downloads the latest **NWPS Gauge Report** from NOAA and filters out irrelevant data.

### **3️⃣ Processing Steps**  
- Removes stations with missing USGS IDs.  
- Filters out stations from **Hawaii (HI), Alaska (AK), and Puerto Rico (PR)**.  
- Excludes known **coastal gauges** to avoid tidal influences.  
- Uses **multi-threading** to speed up data retrieval from USGS.  
- Identifies the **maximum river stage recorded** and assigns a flood category.  
- Performs a **spatial join** with **HUC-8 watershed shapefiles** to link stations to their respective watersheds.  

### **4️⃣ Output Files**  
- **CSV File**: `flood_history_NHA2024.csv`  
  - Contains extracted flood data with river stages, locations, and flood status.  
- **Map Image**: `usgs_site_status_map_conus.png`  
  - A **color-coded** map showing flood statuses across the US.  

---

## **🗺️ Output Data Format (CSV)**  

| USGS ID | NWS LID | Lat | Lon | Max Status | Max Stage | Crest Date | Action Stage | Minor Stage | Moderate Stage | Major Stage | HUC 8 Name | HUC 8 ID |
|---------|--------|-----|-----|------------|----------|------------|--------------|-------------|---------------|------------|------------|-----------|
| 123456  | XYZ1   | 39.5 | -77.5 | Minor | 12.5 | 2024-04-15 | 8.0 | 10.0 | 15.0 | 18.0 | Potomac River | 207001 |

- **Max Status**: The highest flood category observed (`action`, `minor`, `moderate`, `major`, or `none`).  
- **HUC 8 Name/ID**: Hydrologic Unit Code (HUC) region where the gauge is located.  

---

## **📍 Map Visualization**  
The **`usgs_site_status_map_conus.png`** file provides a **CONUS-wide** visualization of flood statuses:  

- **🟡 Yellow** → Action Stage  
- **🟠 Orange** → Minor Flood  
- **🔴 Red** → Moderate Flood  
- **🟣 Purple** → Major Flood  

---

## **⚡ Performance Optimization**
- **Multi-threading** speeds up data retrieval.  
- **Data filtering** reduces unnecessary processing.  
- **Shapefile spatial join** adds watershed information efficiently.  

---

## **📞 Contact & Support**  
For any issues, reach out via GitHub.

🚀 **Happy Flood Tracking!** 🌊
