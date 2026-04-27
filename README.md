# Project-Singapore-Port-Full-Maritime-Data-Ecosystem ⚓
This project is a full-stack maritime data solution system including ETL pipeline (Data Engineering), analyzing vessel congestion and delays (Data Analysis), prediction of vessel delays ML model (Data Science) and interactive business intelligence (BI Development), all created by one person using Singapore Port AIS dataset.

## Contents

1. ETL Pipeline 
2. Delay Prediction ML Model
3. Interactive Dashboard (Tableau)
4. Vessel Congestion and Delays Analysis

## Project Overview

### Project Timeline
* Phase 1: Planning (1 day)
* Phase 2: ETL Pipeline (2 days)
* Phase 3: Dashboard (2 days)
* Phase 4: ML Model building (3 days)
* Phase 5: Data Analysis Report (3 days)

Interactive View - [Project Singapore Port Draw.io](https://drive.google.com/file/d/1INofQiGs57fEAkAdjQJF3ckqFlEtzDZ_/view?usp=sharing)
(Please open with draw.io to achieve interactive view)

![alt image](https://github.com/yanheinaung23-eng/Project-Singapore-Port-Full-Maritime-Data-Ecosystem/blob/07666f0cbe0533047a385d52d9862682a16edaac/Documents/Project%20Final%20Layout.png)

## About the Author
Hi everyone!👋👋 My name is Yan, and I am a former seafarer with professional experience on merchant ships and superyachts. I am currently pursuing a career in data analytics, fueled by a deep passion for leveraging data to solve real-world problems.

By combining my maritime domain knowledge with technical analytics, I aim to support maritimers and port authorities through data-driven systems. As a major step toward this goal, I have built a comprehensive data ecosystem for the Singapore Port, featuring an automated ETL pipeline, a vessel delay prediction model, and congestion and delay interactive dashboard and reports. Hope to enjoy my project and feel free to connect with me!🚢🌊

## About the Dataset
Data Period - 1 October 2023 – 31 October 2023

Dataset used - [AIS Data from 11 ports around the globe – Singapore port](https://research-portal.st-andrews.ac.uk/en/datasets/ais-data-from-11-ports-around-the-globe/)



Using Automatic Identification System (AIS) data from October 2023, I tracked 600k+ vessel observations across 5,877 unique ships over 30 days of dataset from University of St Andrews, Scotland, created by Andreas Hadjipieris (Creator), Neofytos Dimitriou (Creator) Oggie Arandelovic (Creator) School of Computer Science.

Scope
609,468 AIS records  —  5,877 unique vessels  —  14 vessels types

__________________________________________________________________________
## 1. ETL Pipeline ⚙️
![alt image](https://github.com/yanheinaung23-eng/Project-Singapore-Port-Full-Maritime-Data-Ecosystem/blob/72704287f8bffd0456b5ed7e0e384564c6630a1b/Documents/ETL%20Pipeline.png)

### 1.1 Data Ingestion (Bronze Layer) 🥉
The workflow begins with ingesting raw data from the source into the data warehouse. Process:

- Created table with same number of columns as an original data source. [sql script](https://github.com/yanheinaung23-eng/Project-Singapore-Port-Full-Maritime-Data-Ecosystem/blob/72704287f8bffd0456b5ed7e0e384564c6630a1b/ETL%20Pipeline/Bronze%20Layer/Creating%20table%20in%20Bronze%20layer.sql)
- Load data into SQL Server using TRUNCATE and BULK INSERT operations
- Store data in the Bronze layer without transformation and created stored procedure using CREATE OR ALTER, BEGIN TRY to handle errors. [sql script](https://github.com/yanheinaung23-eng/Project-Singapore-Port-Full-Maritime-Data-Ecosystem/blob/72704287f8bffd0456b5ed7e0e384564c6630a1b/ETL%20Pipeline/Bronze%20Layer/Stored%20Procedure%20for%20loading%20raw%20data%20into%20Bronze%20layer.sql)

### 1.2 Data Processing & Standardization (Silver Layer) 🥈
After ingestion, data is transformed in the Silver layer to improve quality and consistency. Process:

- Created table with same number of columns as an original data source. [sql script](https://github.com/yanheinaung23-eng/Project-Singapore-Port-Full-Maritime-Data-Ecosystem/blob/439fce005433b885a32221b0a8bbcd2c4e940995/ETL%20Pipeline/Silver%20Layer/Creating%20table%20in%20Silver%20layer.sql)
- Checking data quality and outliers before loading into Silver Layer. [sql script](https://github.com/yanheinaung23-eng/Project-Singapore-Port-Full-Maritime-Data-Ecosystem/blob/439fce005433b885a32221b0a8bbcd2c4e940995/ETL%20Pipeline/Silver%20Layer/Checking%20data%20quality%20and%20outliers%20before%20loading%20into%20Silver%20layer.sql)
- Transforming inconsistent data and correct them.
- Load cleaned data in the Silver layer using Stored procedure, TRUNCATE and INSERT INTO. [sql script](https://github.com/yanheinaung23-eng/Project-Singapore-Port-Full-Maritime-Data-Ecosystem/blob/439fce005433b885a32221b0a8bbcd2c4e940995/ETL%20Pipeline/Silver%20Layer/Stored%20Procedure%20for%20loading%20cleaned%20data%20into%20Silver%20layer.sql)

### 1.3 Data Integration (Gold Layer) 🥇
This is the final stage, transform data and create view as a gold layer for business ready usage. Process:

- Logical Transformation: Specialized SQL Views translate technical AIS codes into human-readable vessel types and navigational statuses.
- Feature Engineering: Added calculated columns such as week_number and direction (N, NE, E, etc.) for immediate downstream usage. [sql script](https://github.com/yanheinaung23-eng/Project-Singapore-Port-Full-Maritime-Data-Ecosystem/blob/c055f24313352ed86bce17869a5dd88f5534c99f/ETL%20Pipeline/Gold%20Layer/Creating%20View%20in%20Gold%20layer.sql)

### 1.4 Documentation (log for cleaning data in ETL process) 📄
Implemented a comprehensive Data Cleaning Log to ensure pipeline transparency, documenting the audit and correction of maritime-specific anomalies such as ETA inconsistencies and invalid vessel heading values. [log](https://github.com/yanheinaung23-eng/Project-Singapore-Port-Full-Maritime-Data-Ecosystem/blob/7521a25295cda0d480ded07817f5a091dd130fdb/ETL%20Pipeline/Log%20for%20cleaning%20data%20in%20ETL.docx)
____________________________________________________
## 2. Delay Prediction ML Model

The model is Random Forest classifier developed to predict vessel arrival delays at Singapore Port. The model was trained on AIS (Automatic Identification System) vessel tracking data containing 609,468 records from October–December 2023.

The model achieved 77.05% accuracy and an AUC-ROC of 85.36% on unseen test data. The model is capable of predicting whether a vessel will arrive later than its ETA with high reliability, making it suitable for real-time port operations decision support.


Vessel Delay Prediction ML Model (Random Forest) - [Full Python Script](https://github.com/yanheinaung23-eng/Project-Singapore-Port-Full-Maritime-Data-Ecosystem/blob/ed0bf148e0a4959601204a420b7097842e8b9704/Delay%20Prediction%20ML%20Model/Vessel%20Delay%20Prediction%20Model%20(Random%20Forest).ipynb)

Testing Delay Vessel to the Model                - [Full Python Script](https://github.com/yanheinaung23-eng/Project-Singapore-Port-Full-Maritime-Data-Ecosystem/blob/ed0bf148e0a4959601204a420b7097842e8b9704/Delay%20Prediction%20ML%20Model/Testing%20Vessel%20Delay%20Prediction%20Model.ipynb)

![alt image](https://github.com/yanheinaung23-eng/Project-Singapore-Port-Full-Maritime-Data-Ecosystem/blob/bb0f88ea7669f2f6710628ecae388956a51605fb/Delay%20Prediction%20ML%20Model/ML%20Model%20Layout.png)

### 2.1 Confusion Matrix
The confusion matrix below shows prediction outcomes across 176,353 test records:

![alt image](https://github.com/yanheinaung23-eng/Project-Singapore-Port-Full-Maritime-Data-Ecosystem/blob/e0eeceb46aedcf8896a0787db08be71630ef90f3/Delay%20Prediction%20ML%20Model/Confusion%20Matrix%20Layout.png)

### 2.2 Features and their feature importance
Feature importance scores measure how much each variable contributed to the model's decisions, computed as the mean Gini impurity decrease across all 100 trees.

![alt image](https://github.com/yanheinaung23-eng/Project-Singapore-Port-Full-Maritime-Data-Ecosystem/blob/1fe91948c34dc7090edc79c139c1a3bc98100e33/Delay%20Prediction%20ML%20Model/features%20and%20their%20importance.png)

### 2.3 Classification Report
![alt image](https://github.com/yanheinaung23-eng/Project-Singapore-Port-Full-Maritime-Data-Ecosystem/blob/7e81e5faa23bfa9d189ff859e6fe5c9611642a30/Delay%20Prediction%20ML%20Model/classification%20report%20random%20forest.png)

The model is well-balanced; it is slightly more reliable at identifying on-time arrivals (0.80 F1-score) while maintaining solid performance for identifying delays (0.73 F1-score).

### 2.4 Testing the Model
The test example simulating a moored cargo vessel on a Friday—the model successfully processed diverse inputs including speed, draught, and navigational status to determine a 48.0% probability of delay, resulting in an "ON TIME" classification. [Full Script](https://github.com/yanheinaung23-eng/Project-Singapore-Port-Full-Maritime-Data-Ecosystem/blob/ed0bf148e0a4959601204a420b7097842e8b9704/Delay%20Prediction%20ML%20Model/Testing%20Vessel%20Delay%20Prediction%20Model.ipynb)

![alt image](https://github.com/yanheinaung23-eng/Project-Singapore-Port-Full-Maritime-Data-Ecosystem/blob/bd701a23573930742d0eca3f01d7d0bec0079da0/Delay%20Prediction%20ML%20Model/Example%20Prediction%20.png)

### 2.5 Limitation ( No Weather APIs) ⚠️
The model was developed using a specific historical AIS dataset from the University of St Andrews covering October 2023. Because historical weather APIs often require separate premium subscriptions for precise coordinate-based matching back-dated to 2023, the model focuses on high-impact operational features like week_number, eta_hour, and maximum_draught.

### 2.6 Model Performance Report
Finally, I have concluded with the easy-to-follow performance report of my prediction model.
Here is the full report of my model - [Full Report](https://github.com/yanheinaung23-eng/Project-Singapore-Port-Full-Maritime-Data-Ecosystem/blob/1cc925aa03f404f7d65b74bf83dea3a5d0908e3d/Delay%20Prediction%20ML%20Model/Vessel_Delay_Prediction_Model_Report.docx)

_________________________________________________________________
## 3. Interactive Dashboard (Tableau) 📈

Interactive Tableau View - [Singapore Port AIS Traffic & Congestion Analysis Project](https://public.tableau.com/app/profile/yan.aung3461/viz/SingaporePortVesselDelayandCongestionAnalysis/Dashboard1)

![alt image](https://github.com/yanheinaung23-eng/Project-Singapore-Port-Full-Maritime-Data-Ecosystem/blob/97a7724aedf9e5a5d9cf45a4bff66e24a190550f/Interactive%20Dashboard/Dashboard%20Full%20Layout.png)

The Singapore Port AIS Traffic & Congestion Analysis Dashboard is a Tableau-based executive suite for real-time monitoring of port performance. It tracks five core weekly KPIs: Total Vessels, Delay Vessel Count (past ETA), Congestion Level (a weighted index of moored and slow vessels), Moored Vessel Count, and Slow Vessel Identification (moving at ≤5 knots).

The dashboard features an interactive geospatial map that color-codes AIS Activities by status—Anchor, Moored, Underway, or Special—to identify saturation zones and active transit fairways. It also provides granular operational views, including Cargo vs. Tanker navigational comparisons and vessel type distributions via treemaps, with integrated filters for specific weeks and days.

The "calculations" view of the dashboard provides transparency into the logic behind the primary maritime KPIs. It features a detailed breakdown of the formulas used within Tableau to ensure data accuracy and operational relevance.
