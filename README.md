# ☕ Premium Coffee Shop Location Analysis using ArcGIS Pro

<img src="https://github.com/warhazzard/project-premium-coffeeshop-location/blob/main/outputs-images/home_gif.gif?raw=true">

## Project Overview

**Project Scenario:**  
An investor seeks the **best location** to establish a **premium coffee shop** in **Athens, Greece**. This analysis uses **spatial data, crime statistics, and socioeconomic indicators** to find the most suitable neighborhood based on:

- ✅ **High-income population**
- ✅ **Low crime rates**
- ✅ **High foot traffic**
- ✅ **Minimal competition**
- ✅ **Good accessibility (near roads/public transport)**

---

## Study Area & Data Sources

The study is focused on **Athens, Greece**, using:

- **Crime & Socioeconomic data:**  
    Socioeconomic data (Income, Population, etc.), Crime incident locations, postcodes spatial data  
    **Source:** [Cambridge University Press](https://www.cambridge.org/9781108498982)  
    *(Grekousis G. (2020). Spatial analysis theory and practice: describe - explore - explain through GIS. Cambridge University Press, New York, NY)*

- **OpenStreetMap (OSM):**  
    Cafe locations, offices, universities, transport hubs and network, and amenities.

- **ArcGIS Analysis:**  
    Heatmaps, point pattern analysis, spatial autocorrelation and suitability builder.

<p align="center">
<img src="https://github.com/warhazzard/project-premium-coffeeshop-location/blob/main/outputs-images/1_study_area/1_study_area.jpg?raw=true">
</p>

---

## Site Selection Criteria

A **premium coffee store** should be in:

1. **High-income zones** → Customers willing to pay for premium coffee.  
2. **Low-crime areas** → Ensures customer safety.  
3. **High-footfall locations** → Near offices, malls, universities, offices, transit hubs.  
4. **Minimal competition zones** → Avoid oversaturated areas with cafes.  
5. **Easily accessible areas** → Close to subway/bus stations.  

---

## Spatial Analysis Workflow

### 1. <u>Point Pattern Analysis</u>

#### <u>Crime Analysis Using KDE</u>

**Objective:**  
&emsp; Identify high-crime areas to avoid placing the store.

**Tool:**  
&emsp; ArcGIS Pro (`Measure of Spread, Directional Trend - SDE, Ripley's K function, Kernel Density`)

**Output:**  
&emsp; Heatmap of crime hotspots

**Notes:**  
&emsp; To begin the analysis, point data for crimes, assaults, and burglaries was examined to identify any inherent spatial patterns within the city. The primary objective was to locate zones with a relatively higher risk of criminal activity.

To gain a general understanding of the geographical center and directional trend of various crimes, both the geographic mean and the standard deviational ellipse were calculated. In order to determine whether the observed spatial patterns were random or indicative of an underlying clustering phenomenon, an Average Nearest Neighbor analysis was conducted. The results confirmed that the distribution was significantly clustered and unlikely to be due to random chance.

Additionally, Ripley's K function was applied to identify the distance at which clustering was most pronounced. This analysis revealed a dominant clustering distance of approximately 1800 meters, which was subsequently used as the bandwidth parameter for Kernel Density Estimation (KDE) to generate crime hotspots.

The images below illustrate this process step by step.

<p align="center">
    <img src="https://github.com/warhazzard/project-premium-coffeeshop-location/blob/main/outputs-images/2_point_pattern_analysis/1_crime_nearest_neigbour.jpg?raw=true">
</p>

<p align="center">
    <img src="https://github.com/warhazzard/project-premium-coffeeshop-location/blob/main/outputs-images/2_point_pattern_analysis/2_ripley's-K_graph.jpg?raw=true">
</p>

<p align="center">
    <img src="https://github.com/warhazzard/project-premium-coffeeshop-location/blob/main/outputs-images/2_point_pattern_analysis/2_ripley's-K_table.jpg?raw=true">
</p>

<p align="center">
    <img src="https://github.com/warhazzard/project-premium-coffeeshop-location/blob/main/outputs-images/2_point_pattern_analysis/3_crime_risk.jpg?raw=true">
</p>

---

#### <u>Supply & Demand Analysis</u>

**Objective:**  
&emsp; Identify ideal locations based on:

- **Existing coffee shops** (Avoid high competition areas)  
- **Footfall zones** (Universities, malls, offices)

**Tool:**  
&emsp; ArcGIS (`Proximity(Buffer), Measure of Spread, Directional Trend & Kernel Density Analysis`)

**Output:**  
&emsp; Heatmap of Supply and Demand

**Notes:**  
&emsp; Following a similar point pattern analysis approach used for crime data, the spatial distribution of existing cafés and coffee shops (representing Supply) was analyzed alongside targeted foot traffic groups (representing Demand). The objective was to identify areas of alignment—or mismatch—between café locations and high-demand zones.

The images below illustrate the identified Supply and Demand hotspots.


<p align="center">
    <img src="https://github.com/warhazzard/project-premium-coffeeshop-location/blob/main/outputs-images/2_point_pattern_analysis/4_demand.jpg?raw=true">
</p>

<p align="center">
    <img src="https://github.com/warhazzard/project-premium-coffeeshop-location/blob/main/outputs-images/2_point_pattern_analysis/5_supply.jpg?raw=true">
</p>


---

### 2. Spatial Autocorrelation

#### Locating High-Income Areas

**Objective:**  
&emsp; Identify high-income areas for our store.

**Tool:**  
&emsp; ArcGIS Pro (`Moran’s I, Getis-Ord General G`)

**Output:**  
&emsp; Identify spatial autocorrelation of Income

**Notes:**  
&emsp; To explore spatial patterns in income distribution, a series of spatial statistical analyses were conducted.

First, a threshold distance was identified for calculating Global Moran’s I, which provided insight into the overall spatial autocorrelation of income levels across the city. Using this distance, a spatial weights matrix was created to serve as the foundation for further local analyses.

Next, Local Moran’s I was applied to detect the presence of income-based clusters and outliers. This helped answer the key question: Are there localized clusters or anomalies in income distribution, and where are they located?

Finally, Local Getis-Ord G* analysis was performed to pinpoint statistically significant income hotspots and coldspots, offering a clear visual of areas with concentrated high or low income levels. 

<p align="center">
    <img src="https://github.com/warhazzard/project-premium-coffeeshop-location/blob/main/outputs-images/3_spatial_autocorrelation/1_moranI-global.jpg?raw=true">
</p>

<p align="center">
    <img src="https://github.com/warhazzard/project-premium-coffeeshop-location/blob/main/outputs-images/3_spatial_autocorrelation/2_h_l-clustering-generel%20getis%20ord%20g.jpg?raw=true">
</p>

<p align="center">
    <img src="https://github.com/warhazzard/project-premium-coffeeshop-location/blob/main/outputs-images/3_spatial_autocorrelation/3_incremental-moran'sI.jpg?raw=true">
</p>

<p align="center">
    <img src="https://github.com/warhazzard/project-premium-coffeeshop-location/blob/main/outputs-images/3_spatial_autocorrelation/4_local_morans-i_outlier_and_cluster.jpg?raw=true">
</p>

<p align="center">
    <img src="https://github.com/warhazzard/project-premium-coffeeshop-location/blob/main/outputs-images/3_spatial_autocorrelation/5_hotspots-coldspots.jpg?raw=true">
</p>

---

#### Multivariate Analysis: Clustering

**Objective:**  
Clustering – High spenders, locating high-income areas, and determining the best location.

**Tool:**  
ArcGIS Pro (`Group Analysis(K-means), Cosine Similarity`)

**Output:**  
Best candidate postcodes for store location

- Multivariate Analysis  
- Similarity Analysis  

<p align="center">
    <img src="https://github.com/warhazzard/project-premium-coffeeshop-location/blob/main/outputs-images/3_spatial_autocorrelation/6_multivar_kmeans.jpg?raw=true">
</p>

<p align="center">
    <img src="https://github.com/warhazzard/project-premium-coffeeshop-location/blob/main/outputs-images/3_spatial_autocorrelation/7_psedo_f-statistic.jpg?raw=true">
</p>

<p align="center">
    <img src="https://github.com/warhazzard/project-premium-coffeeshop-location/blob/main/outputs-images/3_spatial_autocorrelation/8_similarity_analysis.jpg?raw=true">
</p>

---

### 3. Identifying Locations with Ease-of-Accessibility

**Objective:**  
Accessibility Buffer

**Tool:**  
ArcGIS Pro (`Buffer`)

**Output:**  
Accessibility Raster

<p align="center">
    <img src="https://github.com/warhazzard/project-premium-coffeeshop-location/blob/main/outputs-images/4_accessibility/1_accessibility.jpg?raw=true">
</p>

---

### 4. Suitability Analysis

**Objective:**  
To finally find the best postcode for our premium coffee shop.

**Tool:**  
ArcGIS (`Suitability Modeler`)

**Output:**  
Map showing best postcodes suitable for our premium coffee shop.

<p align="center">
    <img src="https://github.com/warhazzard/project-premium-coffeeshop-location/blob/main/outputs-images/5_suitability-analysis/1_Suitability_Map.jpg?raw=true">
</p>

<p align="center">
    <img src="https://github.com/warhazzard/project-premium-coffeeshop-location/blob/main/outputs-images/5_suitability-analysis/2_Best_postcode.jpg?raw=true">
</p>
