# Project-Singapore-Port-Full-Maritime-Data-Ecosystem ⚓
This project is a full-stack maritime data solution system including ETL pipeline (Data Engineering), analyzing vessel congestion and delays (Data Analysis), prediction of vessel delays ML model (Data Science) and interactive business intelligence (BI Development), all created by one person using Singapore Port AIS dataset.

# About the Author
Hi everyone!👋👋 My name is Yan, and I am a former seafarer with professional experience on merchant ships and superyachts. I am currently pursuing a career in data analytics, fueled by a deep passion for leveraging data to solve real-world problems.

By combining my maritime domain knowledge with technical analytics, I aim to support maritimers and port authorities through data-driven systems. As a major step toward this goal, I have built a comprehensive data ecosystem for the Singapore Port, featuring an automated ETL pipeline, a vessel delay prediction model, and congestion and delay interactive dashboard and reports. Hope to enjoy my project and feel free to connect with me!🚢🌊

## Contents

1. ETL Pipeline 
2. Delay Prediction ML Model
3. Interactive Tableau Dashboard
4. Vessel Congestion and Delays Analysis

## Project Overview

### Project Timeline
* Phase 1: Planning (1 day)
* Phase 2: ETL Pipeline (2 days)
* Phase 3: Dashboard (2 days)
* Phase 4: ML Model building (3 days)
* Phase 5: Data Analysis Report (3 days)

Interactive View - [Project Singapore Draw.io](https://drive.google.com/file/d/1INofQiGs57fEAkAdjQJF3ckqFlEtzDZ_/view?usp=sharing)

![alt image](https://github.com/yanheinaung23-eng/Project-Singapore-Port-Full-Maritime-Data-Ecosystem/blob/07666f0cbe0533047a385d52d9862682a16edaac/Documents/Project%20Final%20Layout.png)
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

