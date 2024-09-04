# ANALYSIS ON CLIMATE CHANGE

The primary aim of this project is to create a model that will be useful in predicting the patterns in environmental change in different areas of the world in the coming years and to utilize this data to study weather conditions, explicitly as to temperature, precipitation, and irregularities. We will also analyze the connection between the current shift in weather patterns and the historical production of carbon emissions by various countries. By expanding our understanding of climate change, extreme weather, and regional variations, the project aims to advance climate science. This will assist with asset portion, debacle planning, and environment variation independent direction, eventually encouraging strength and maintainability.

### Solution Approach

The approach of this project is that it provides this platform where all kinds of analyzing are readily available to understand and predict the climate changes. Here, we are going develop a predictive model using a pipeline with various google cloud services that helps in transforming the data , including real-time data into the warehouse and finally create a predictive model.

### Pipeline using the google cloud services

The data is first present in the VPC which is then sent to the big query using the data stream. Now this data is stored in the staging database in the big query. The warehouse is created using this staging database. On the other hand, the real-time data is sent through the API which is processed and scheduled to various transformations using airflow. This ETL is runned in cloud composer. This data is scheduled on daily basis and send to the warehouse. Now that the data is stored in the warehouse, we can perform various analysis and create a model to predict the future climate conditions. This data can be even used to perform visualizations using tableau.

![image](https://github.com/user-attachments/assets/af4c83cc-23d6-4adc-b46b-0bc6555e344e)

### Data Sources

There are two different types of data sources for this project. One is the archived data which is extracted from various websites. The other data source is real-time data which is updated on daily bases.
1.	Daily climate data from https://www.kaggle.com/datasets/guillemservera/global-daily-climate-data/data . This dataset is regularly updated from the Meteostat API, comprising        three key data frames: Cities, Countries, and Daily Weather. Cities provide details about weather stations, while Countries offer demographic insights on countries.
2.	Current weather-temperature data feed from  https://open-meteo.com/
3.	Real time weather data from https://openweathermap.org/api
4.	Cumulative greenhouse gas emission data from different nations from https://zenodo.org/record/7636699#.ZFCy4exBweZ . National contributions to climate change due to historical      emissions of carbon dioxide, methane and nitrous oxide data consists of following files.

### ELT Process

Virtual private cloud(VPC) is created on GCP platform with SQL cloud instance.Using DataStream archived data is transferred from VPC to BigQuery table. Raw archived data is first loaded to Big Query staging tables.

### Datawarehouse Design

Datawarehouse helps in storing the data that is centralized and can intergrate different kinds of data. It is also mostly used to store archived data on which analytics are performed. For this project BigQuery is used to build datawarehouse and Star Schema structure is  designed.
The raw data which is sent through the data stream is fetched and saved under one dataset called climate- data-staging. From this dataset, the data is transformed into star schema, performing various operations like changing the datatypes of the columns, expanding the date column and so on.
climate_fact - a fact table along with 4 primary dimension tables are created

### Airflow for Real time data 

For this project, the Apache airflow is used to create DAGs to define, schedule and execute a few tasks in a pipeline.Using DAG we extracts the data from openweather API for a particular list of cities. 
After extracting it validates the retrieved data, checks if there are any missing or errors in the data. It then processes the data after either correcting or filling of the data, subsequently updates the table in Big Query with the number of records or missing records. This raw data is then structured into a data frame including changing few column datatypes to appropriate types.At the end data is loaded into a staging database.

### Data Analysis and Visualization

Exploratory data analysis is performed using BigQuery and visualization is done using Tableau.

### Predictive model using BIG QUERY

For this project, we were able to perform time series to predict the future weather reports based on the archived data information.
ARIMA model - In Big Query, with the Machine learning functions time series analysis is performed. Using max temperature as the target variable and the record date as the timestamp, AutoRegressive Integrated moving average time series analysis is done.The model is being evaluated using various metrices - mean absolute error , mean squared error
