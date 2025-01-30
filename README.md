# **Motor Vehicle Collision Analysis**

## **Project Overview**
Worked with over 3 million records in developing a motor vehicle collision analysis platform based on accidents occured in Austin, Chicago, Montgomery and New York City using government provided datasets. The project involved data profiling, standardizing and integrating data from multiple sources with different schemas, followed by dimensional modeling to organize data into facts and dimensions. Interactive dashboards were designed to provide insights into accident trends, high-risk areas, temporal analysis, injury patterns and contributing factors.

- Tools Used: Alteryx, Microsoft Excel, Azure Data Factory, Talend, ER Studio, Snowflake, SQL, PowerBI, Tableau 


## **Datasets Overview**
The analysis is based on publicly available **motor vehicle collision datasets** from city government sources:  

| **City**      | **Source** |
|--------------|------------|
| **Austin**   | [Austin Data](https://data.austintexas.gov/Transportation-and-Mobility/Austin-Crash-Report-Data-Crash-Level-Records/y2wy-tgr5/about_data) |
| **Chicago**  | [Chicago Data](https://data.cityofchicago.org/Transportation/Traffic-Crashes-Crashes/85ca-t3if/about_data) |
| **NYC**      | [NYC Data](https://data.cityofnewyork.us/Public-Safety/Motor-Vehicle-Collisions-Crashes/h9gi-nx95/about_data) |
| **Montgomery** | [Montgomery Data](https://data.montgomerycountymd.gov/Public-Safety/Crash-Reporting-Incidents-Data/bhju-22kf/about_data) |


## **Business Requirements**

### **1. Accident Statistics**
- **Total Accidents**: Breakdown by city (NYC, Austin, Chicago, Montgomery).
- **High-Risk Areas**: Identify **top 3 accident-prone locations** per city.

### **2. Injury & Pedestrian Involvement**
- **Injury Analysis**:
  - Number of accidents that resulted **only in injuries**.
  - Reports available **overall** and **by city**.
- **Pedestrian Accidents** (Chicago-specific analysis).

### **3. Time-Based Accident Trends**
- **Seasonality Trends**: When do **most accidents occur** (Winter, Spring, Summer, Fall)?
- **Time Analysis**:
  - **Time of day** (Morning, Afternoon, Night).
  - **Day of the week**, **Weekday vs. Weekend** trends.

### **4. Motorist & Fatality Analysis**
- **Motorist Injuries & Fatalities** (overall and city-level breakdown).
- **Top 5 Locations with most fatal accidents** in all cities.
- **Pedestrian vs. Motorist Fatality Comparison**.

### **5. Contributing Factors**
- **Most Common Causes of Accidents**

## **Project Steps**
### **1. Understanding the Dataset & Business Requirements**
- Examined all datasets to understand schema variations.
- Analyzed **business questions** to determine required transformations and prepared a plan of execution.

### **2. Data Profiling & As-Is Staging**
- **Alteryx** was used to perform **data profiling**, identifying:
  - **Data types, missing values, and anomalies**.
- **Azure Data Factory (ADF)** was used to stage raw data.
- Implemented the **Medallion Architecture**:
  - **Bronze Layer**: Ingested raw CSV and TSV files without modifications.
  - **Silver Layer**: Converted the source files to **Parquet format**.
  - **Gold Layer**: Converted the Parquet data and stored them in Snowflake as tables.

### **3. Data Transformation**
- Created a **Mapping Document**:
  - Identified fields required to address business requirements.
  - Mapped transformations across datasets to **ensure schema consistency**.
- **Talend** was used for data transformation:
  - Filling missing values (**-9999** for numerical, **‘NA’** for text).
  - Extracted meaningful attributes by splitting single columns into multiple and merging related columns as per mapping document
  - Removed junk text and irrelevant characters using regex patterns to enhance data quality.
  - Capitalized all text for consistency, applied uniform decimal precision, and standardized timestamps to the desired format.
  - Adjusted column values with zero-padding or truncation to ensure uniformity across datasets.
  - Derived additional attributes to meet business requirements through calculated fields.
  - Added audit columns for traceability.
  - Loaded the transformed data into a final staging table in Snowflake, ensuring readiness for dimensional modeling.

### **4. Dimensional Modeling**
- Designed a **dimensional model** using **ER Studio**:
  - Created **Fact & Dimension tables** in a **Snowflake Schema**.
  - Implemented **Slowly Changing Dimension (SCD) Type 2**, as per business logic.

### **5. Loading of Data into Facts & Dimensions**
- Loaded data into the dimensional model in Snowflake using Talend.
- Added audit columns to ensure data traceability.

### **6. Visualization & Dashboard Design**
- **Power BI & Tableau Dashboards**:
  -  Focused on creating dashboards that are simple, clean, and highly functional for end-users.
  - **Title & Filters** positioned at the **top** for usability.
  - **KPIs placed prominently** in the top-left.
  - Ensured Tableau and Power BI dashboards mirrored each other in design, enabling business partners to switch between platforms seamlessly based on their convenience.
- **Geospatial Mapping**:
  - Plotted latitude/longitude of accidents for location analysis.

