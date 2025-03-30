# ☕ Premium Coffee Shop Location Analysis using ArcGIS Pro

![Study Area](outputs-images/1_study_area/home_gif.gif)

## 📌 Project Overview

**Project Scenario:** An investor seeks the **best location** to establish a **premium coffee shop** in **Athens, Greece**. This analysis uses **spatial data, crime statistics, and socioeconomic indicators** to find the most suitable neighborhood based on:
- ✅ **High-income population**
- ✅ **Low crime rates**
- ✅ **High foot traffic**
- ✅ **Minimal competition**
- ✅ **Good accessibility (near roads/public transport)**

## 📍 **Study Area & Data Sources**

The study is focused on **Athens, Greece**, using:
- **Crime & Socioeconomic data:** Socioeconomic data (Income, Population, etc.), Crime incident locations, postcodes spatial data **source:** - (www.cambridge.org/9781108498982) (Grekousis G. (2020). Spatial analysis theory and practice: describe - explore - explain through GIS. Cambridge University Press, New York, NY)
- **OpenStreetMap (OSM):** Cafe locations, offices, universities, transport hubs and network, and amenities.
- **ArcGIS Analysis:** Heatmaps, point pattern analysis, and suitability scores.

![[study area 1.jpg]]

## 🔍 **Site Selection Criteria**

A **premium coffee store** should be in:
1. **High-income zones** → Customers willing to pay for premium coffee.
2. **Low-crime areas** → Ensures customer safety.
3. **High-footfall locations** → Near offices, malls, universities, offices, transit hubs.
4. **Minimal competition zones** → Avoid oversaturated areas with cafe.
5. **Easily accessible areas** → Close to subway/bus stations.

## 🏗 **Spatial Analysis Workflow**

### **Point Pattern Analysis:**

#### **1️⃣ Crime Analysis Using KDE**
**Objective:** Identify high-crime areas to avoid placing the store.

📌 **Tool:** ArcGIS Pro (`Measure of Spread, Directional Trend - SDE, Ripley's K function, Kernel Density`)

🔹 **Output:** Heatmap of crime hotspots

![Crime KDE](docs/images/crime_kde.png)

---

#### **2️⃣ Competitor & Demand Analysis**
**Objective:** Identify ideal locations based on:

- **Existing coffee shops** (Avoid high competition areas)
- **High Accessibility** (Proximity to transport hubs)
- **Footfall zones** (Universities, malls, offices)

📌 **Tool:** ArcGIS (`Proximity(Buffer), Measure of Spread, Directional Trend & Kernel Density Analysis`)

🔹 **Output:** Heatmap of Supply and Demand


### **Spatial Autocorrelation:**

#### **1️⃣ Locating High-Income Areas**

**Objective:** Identify high-income areas for our store.

📌 **Tool:** ArcGIS Pro (`Moran’s I, Getis-Ord General G`)

🔹 **Output:** Indentify spatial autocorrelation of Income

- Identifying threshold distance for global Moran's I
- Estimating spatial weights table based on the previously estimated distance to be used in cluster and outlier analysis to identify local income clusters and hotspots
- Examining if local clusters and outliers exists, and if so where are they? - using local Moran's I 
- Finally, identify income hotspots and coldspots using the local Getis-Ord G∗


#### **2️⃣ Multivariate Analysis: Clustering**

**Objective:** Clustering – High spenders, locating high income areas and determining best location

📌 **Tool:** ArcGIS Pro (`Group Analysis(K-means), Cosine Similarity`)

🔹 **Output:** Best candidates postcodes for store location

- Multivariate Analysis
- Similarity Analysis

### **Identifying locations with Ease-of-Accessibility:**

**Objective:** Accessibility Buffer

📌 **Tool:** ArcGIS Pro (`Buffer`)

🔹 **Output:** Accessibility Raster

### **Suitability Analysis:**