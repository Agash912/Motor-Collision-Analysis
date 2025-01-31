# Motor Vehicle Collision Analysis

## Project Overview
Worked with over 3 million records in developing a motor vehicle collision analysis platform based on accidents occured in Austin, Chicago, Montgomery and New York City using government provided datasets. The project involved data profiling, standardizing and integrating data from multiple sources with different schemas, followed by dimensional modeling to organize data into facts and dimensions. Interactive dashboards were designed to provide insights into accident trends, high-risk areas, temporal analysis, injury patterns and contributing factors.

Tools Used: Alteryx, Microsoft Excel, Azure Data Factory, Talend, ER Studio, Snowflake, SQL, PowerBI, Tableau 


## Datasets Overview
The analysis is based on publicly available motor vehicle collision datasets from city government sources:  

| City      | Source |
|--------------|------------|
| Austin   | [Austin Data](https://data.austintexas.gov/Transportation-and-Mobility/Austin-Crash-Report-Data-Crash-Level-Records/y2wy-tgr5/about_data) |
| Chicago  | [Chicago Data](https://data.cityofchicago.org/Transportation/Traffic-Crashes-Crashes/85ca-t3if/about_data) |
| NYC      | [NYC Data](https://data.cityofnewyork.us/Public-Safety/Motor-Vehicle-Collisions-Crashes/h9gi-nx95/about_data) |
| Montgomery | [Montgomery Data](https://data.montgomerycountymd.gov/Public-Safety/Crash-Reporting-Incidents-Data/bhju-22kf/about_data) |


## Business Requirements

### 1. Accident Statistics
- Total Accidents: Breakdown by city (NYC, Austin, Chicago, Montgomery).
- High-Risk Areas: Identify top 3 accident-prone locations per city.

### 2. Injury & Pedestrian Involvement
- Injury Analysis:
  - Number of accidents that resulted only in injuries.
  - Reports available overall and by city.
- Pedestrian Accidents (Chicago-specific analysis).

### 3. Time-Based Accident Trends
- Seasonality Trends: When do most accidents occur (Winter, Spring, Summer, Fall)?
- Time Analysis:
  - Time of day (Morning, Afternoon, Night).
  - Day of the week, Weekday vs. Weekend trends.

### 4. Motorist & Fatality Analysis
- Motorist Injuries & Fatalities (overall and city-level breakdown).
- Top 5 Locations with most fatal accidents in all cities.
- Pedestrian vs. Motorist Fatality Comparison.

### 5. Contributing Factors
- Most Common Causes of Accidents

## Project Steps
### 1. Understanding the Dataset & Business Requirements
- Examined all datasets to understand schema variations.
- Analyzed business questions to determine required transformations and prepared a plan of execution.

### 2. Data Profiling & As-Is Staging
- Alteryx was used to perform data profiling, identifying data types, missing values, and anomalies.
    ### Pipeline created for profiling (Eg. Austin):
    ![image](https://github.com/user-attachments/assets/ba96054a-7e28-4796-878e-9ffb6f046b0c)


- Azure Data Factory (ADF) was used to stage raw data and Medallion Architecture was implemented:
  - Bronze Layer: Ingested raw CSV and TSV files without modifications.
  - Silver Layer: Converted the source files to Parquet format.
  - Gold Layer: Converted the Parquet data and stored them in Snowflake as tables.
    ### Pipeline created in Azure (Eg. Austin):
    ADF:
    ![image](https://github.com/user-attachments/assets/83373a8a-6af5-4a99-9bc4-cfd8804becf8)

    Dataflow:
    ![image](https://github.com/user-attachments/assets/31c13bd5-228e-4631-9ed2-55f2d16cc169)



### 3. Data Transformation
- Created a Mapping Document:
  - Identified fields required to address business requirements.
  - Mapped transformations across datasets to ensure schema consistency.
- Talend was used for data transformation:
  - Filled missing values (-9999 for numerical, ‘NA’ for text), after attempting to replace them by computing from other available columns.
  - Extracted meaningful attributes by splitting single columns into multiple and merging related columns as per mapping document
  - Removed junk text and irrelevant characters using regex patterns to enhance data quality.
  - Capitalized all text for consistency, applied uniform decimal precision, and standardized timestamps to the desired format.
  - Adjusted column values with zero-padding or truncation to ensure uniformity across datasets.
  - Derived additional attributes to meet business requirements through calculated fields.
  - Added audit columns for traceability.
  - Loaded the transformed data into a final staging table in Snowflake, ensuring readiness for dimensional modeling.
    ### Pipeline created in Talend (Eg. Austin):
    ![image](https://github.com/user-attachments/assets/93fe10ae-aa27-4f08-be0a-cef8cc7460ae)

    T Map overview:
    ![image](https://github.com/user-attachments/assets/7a789439-362e-40b1-ba33-85600fea646d)

    ### Pipeline created to combine all transformed data into one:
    ![image](https://github.com/user-attachments/assets/f7f87233-f12d-4a9f-bc3c-da08186c40bc)


### 4. Dimensional Modeling
- Designed a dimensional model using ER Studio:
  - Created Fact & Dimension tables in a Snowflake Schema.
  - Implemented Slowly Changing Dimension (SCD) Type 2, as per business logic.
  - Generated a physical model and DDL scripts.
  - Executed the scripts in Snowflake to create the dimensional schema.
    
    ### Dimensional Model Prepared:
    ![image](https://github.com/user-attachments/assets/f478a499-82a6-4639-a9b3-22d03a61cc0f)

    SCD Implementation:
    ![image](https://github.com/user-attachments/assets/5b9dd2e3-9673-491d-9b86-dd04cfb6486f)


    
### 5. Loading of Data into Facts & Dimensions
- Loaded data into the dimensional model in Snowflake using Talend.
- Added audit columns to ensure data traceability.

  ![image](https://github.com/user-attachments/assets/b1cb6ebe-c164-4042-b2ef-749ea3e5beba)
  ![image](https://github.com/user-attachments/assets/0871a1de-7c8c-47d8-b3f1-bfa06d949c87)
  ![image](https://github.com/user-attachments/assets/8ab03dbb-b09b-4255-828d-5ff8748dc1fe)
  ![image](https://github.com/user-attachments/assets/9ec4059c-72ee-4390-8a6a-2bada9231cb2)
  ![image](https://github.com/user-attachments/assets/c6478c67-0769-479a-b8ea-13292726cd99)


### 6. Visualization & Dashboard Design
- Design Principles followed::
  -  Focused on creating dashboards that are simple, clean, and highly functional for end-users.
  - Title & Filters positioned at the top for usability.
  - KPIs placed prominently in the top-left.
  - Ensured Tableau and Power BI dashboards mirrored each other in design, enabling business partners to switch between platforms seamlessly based on their convenience.
- Geospatial Mapping:
  - Plotted latitude/longitude of accidents for location analysis.
  ## Power BI:

  ![image](https://github.com/user-attachments/assets/2a48d215-18eb-4c43-b7f2-edc0b5b32248)
  ![image](https://github.com/user-attachments/assets/083d8d68-c3e6-4064-a108-a6a14576cd74)

  ## Tableau:
  
  ![image](https://github.com/user-attachments/assets/de680c12-9532-4462-a855-02eee9671b30)
  ![image](https://github.com/user-attachments/assets/68a5ef2f-e196-4ef7-b9da-a41a59e37111)

The prepared dashboard provide insights to observe trends and patterns of accidents occuring in Austin, Chicago, NYC and Montgomery.
