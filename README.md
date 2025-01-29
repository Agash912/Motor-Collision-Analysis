# **Motor Vehicle Collision Analysis 🚗💥**

## **Project Overview**
This project analyzes **motor vehicle collision data** from four major cities: **Austin, Chicago, Montgomery, and New York City**. The objective is to create an **ETL pipeline** to integrate disparate datasets, perform necessary transformations, and load the processed data into a **dimensional model** for analysis. The final output includes **interactive dashboards in Power BI and Tableau**, providing insights into accident trends, high-risk areas, injury patterns, and contributing factors.

Key objectives:
- Standardizing and integrating data from multiple sources with different schemas.
- Building a structured **data warehouse** using **Snowflake**.
- Implementing **dimensional modeling** to optimize analytics.
- Creating dashboards to visualize accident statistics and patterns.

---

## **Tools & Technologies Used**
The following tools and technologies were used in the project:

| **Component**         | **Tools Used**                     |
|----------------------|--------------------------------|
| **Data Extraction & Staging** | Azure Data Factory (ADF) |
| **Data Profiling**   | Alteryx                        |
| **Data Transformation & Cleaning** | Talend |
| **Data Storage & Warehousing** | Snowflake                     |
| **Dimensional Modeling** | ER Studio                     |
| **Visualization**    | Tableau, Power BI              |

---

## **Datasets Overview**
The analysis is based on publicly available **motor vehicle collision datasets** from city government sources:  

| **City**      | **No. of Columns** | **No. of Rows** | **Source** |
|--------------|-----------------|----------------|------------|
| **Austin**   | 43              | 212,834        | [Austin Data](https://data.austintexas.gov/Transportation-and-Mobility/Austin-Crash-Report-Data-Crash-Level-Records/y2wy-tgr5/about_data) |
| **Chicago**  | 48              | 896,756        | [Chicago Data](https://data.cityofchicago.org/Transportation/Traffic-Crashes-Crashes/85ca-t3if/about_data) |
| **NYC**      | 29              | 2,139,048      | [NYC Data](https://data.cityofnewyork.us/Public-Safety/Motor-Vehicle-Collisions-Crashes/h9gi-nx95/about_data) |
| **Montgomery** | 37             | 107,003        | [Montgomery Data](https://data.montgomerycountymd.gov/Public-Safety/Crash-Reporting-Incidents-Data/bhju-22kf/about_data) |

Key challenges included:
- **Different schemas** across datasets.
- **Varying data formats** and missing values.
- **Ensuring uniformity** while preserving critical information.

---

## **Business Requirements**
The project aims to answer key business questions related to **motor vehicle collisions**, **injury patterns**, and **risk factors**:

### **1. Accident Statistics**
- **Total Accidents**: Breakdown by city (NYC, Austin, Chicago).
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
- **Top 5 Deadliest Locations** in all cities.
- **Pedestrian vs. Motorist Fatality Comparison**.

### **5. Contributing Factors**
- **Most Common Causes of Accidents**:
  - Driver errors (speeding, DUI, distracted driving).
  - Environmental and road conditions.

---

## **Project Steps**
### **1. Understanding the Dataset & Business Requirements**
- Examined all datasets to understand schema variations.
- Analyzed **business questions** to determine required transformations.

### **2. Data Profiling & As-Is Staging**
- **Alteryx** was used to perform **data profiling**, identifying:
  - **Data types, missing values, and anomalies**.
- **Azure Data Factory (ADF)** was used to stage raw data.
- Implemented the **Medallion Architecture**:
  - **Bronze Layer**: Raw source files stored as-is.
  - **Silver Layer**: Converted **Parquet files** stored in Snowflake.

### **3. Data Transformation using Talend**
- Created a **Mapping Document**:
  - Identified **common fields** across datasets.
  - Mapped transformations to **ensure schema consistency**.
- **Talend** was used for data transformation:
  - **Cleansing operations**:
    - Filling missing values (**-9999** for numerical, **‘NA’** for text).
    - Standardizing text capitalization and decimal precision.
  - **TMAP transformations**:
    - Merging and restructuring columns.
    - Formatting dates and categorical values.
  - Combined all datasets into a **final staging table** in Snowflake.

### **4. Dimensional Modeling**
- Designed a **dimensional model** using **ER Studio**:
  - Created **Fact & Dimension tables** in a **Snowflake Schema**.
  - Implemented a **Slowly Changing Dimension (SCD) Type 2**.

### **5. Loading of Data into Facts & Dimensions**
- **Talend** loaded transformed data into:
  - **Fact tables** (e.g., Accidents, Injuries).
  - **Dimension tables** (e.g., Location, Time, Vehicles).
- **Final data stored in Snowflake** for reporting.

### **6. Visualization & Dashboard Design**
- **Power BI & Tableau Dashboards**:
  - **Title & Filters** positioned at the **top** for usability.
  - **KPIs placed prominently** in the top-left.
  - **Consistent design across both platforms** for ease of use.
- **Geospatial Mapping**:
  - Plotted latitude/longitude of accidents for location analysis.

---

## **Conclusion**
This project successfully built a scalable **ETL pipeline** for analyzing motor vehicle collisions across multiple cities. The structured **dimensional model** and **interactive dashboards** enable deeper insights into **accident trends, high-risk areas, and injury patterns**, supporting **data-driven decision-making** for public safety.

---

🚀 **Technologies Used:** Alteryx | Talend | ADF | Azure | Snowflake | ER Studio | Power BI | Tableau  
📊 **Key Concepts:** Data Integration | ETL Pipeline | Dimensional Modeling | Slowly Changing Dimensions | Big Data Processing  
