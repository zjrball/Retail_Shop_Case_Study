# Retail Shop Case Study

## Table of Contents

- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Tools](#tools)
- [Data Cleaning/Preparation](#data-preparation)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Dashboard](#dashboard)
- [Results](#results)
- [Recommendations](#recommendations)
- [Acknowledgement](#acknowledgement)



### Project Overview
This is a retail performance dashboard for a chain of shops in Florida. It visualizes key metrics like total sales, customer numbers, and average sales by city to track performance and identify trends between 2023 and 2024.

### Data Sources

Sales Data: The dataset used for this analysis is the "sales_2yrs.csv" file, within the file are the past two years of sales across multiple stores. 
Survey Data: The dataset used for this analysis is the "survey_2yrs.csv" file, within the file contains demographic information of previous customers.
Weather Data: The dataset used for this analysis is the "weather_2yrs.csv" file, containing information about precipitation and humidity. 

### Tools

- Excel - Data Source
- PowerBI - Data Reporting
- MySQL - Data View/Analysis

### Data Preparation

In order to prepare the data for presentation, I formatted the values within Power Query Editor.

### Exploratory Data Analysis

EDA was performed to answer the following questions:

1. How strongly does temperature and rainfall affect daily sales?
2. Which shop performs best?
3. Who are our customers, families or singles, male versus female, and how does this change over time?
4. Are there predictable seasonal patterns in sales?
5. What actions would you take based on these insights?

### Data Analysis

SQL view created to report on using PowerBI:

```sql
CREATE OR REPLACE VIEW retail.table_joined AS 

SELECT 
s.date,
dayname(date) AS day_of_week,
CASE WHEN weekday(date) IN (5,6) THEN "Weekend" ELSE "Weekday" END AS is_weekend,
s.shop_id,
s.shop_name,
s.customers,
s.sales_usd,
s.sales_usd/s.customers AS sales_per_customer,
su.pct_male,
su.pct_female,
su.pct_family,
su.pct_single,
w.avg_temp_f,
w.precip_in,
w.is_rain,
w.humidity_pct
FROM retail.sales s 
LEFT JOIN retail.survey su USING(date) 
LEFT JOIN retail.weather w USING(date)
```
### Dashboard
<img width="1516" height="852" alt="Screenshot 2025-11-21 141622" src="https://github.com/user-attachments/assets/c1d4af85-0b07-4043-aefa-285d56157eee" />



### Results



### Recommendations


### Acknowledgement:

This project was completed as part of a tutorial. I want to give full credit to the original creator.

* **Author:** [[Absent Data](https://www.youtube.com/@absentdata)]
* **Tutorial:** [[Tutorial Link](https://www.youtube.com/watch?v=Hh5-Y_6v5iU&list=PLi5spBcf0UMXfbMt1X2bHQkk7mHXkTUhs&index=9)]

My goal in completing this project was to familiarize myself with MySQL, PowerBI, and GitHub.




