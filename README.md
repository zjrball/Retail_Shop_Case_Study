# Retail Shop Case Study

## Table of Contents

- [Project Overview](#project-overview)
- [Dashboard](#dashboard)
- [Data Sources](#data-sources)
- [Tools](#tools)
- [Data Cleaning/Preparation](#data-preparation)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Results](#results)
- [Recommendations](#recommendations)
- [Acknowledgement](#acknowledgement)



### Project Overview
This is a retail performance dashboard for a chain of shops in Florida. It visualizes key metrics like total sales, customer numbers, and average sales by city to track performance and identify trends between 2023 and 2024.

### Dashboard
<img width="1516" height="852" alt="Screenshot 2025-11-21 141622" src="https://github.com/user-attachments/assets/c1d4af85-0b07-4043-aefa-285d56157eee" />

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

### Results

## Environmental Impact (Weather):
- Temperature: Sales show a strong positive correlation with temperature; as the temperature rises (especially in Q3 Summer months), sales volume increases.
- Rainfall: Rain is a significant performance dampener. Days with rain see a drastic drop in customer foot traffic (approx. -50% compared to clear days), leading to lower revenue.
  
<img width="983" height="361" alt="image" src="https://github.com/user-attachments/assets/9cbbdcf5-828e-4227-93fa-21d383c9318b" />

## Store Performance:
- Top Performer: The Miami shop is the clear leader in both total revenue and average sales per customer (~$18/customer).
- Rankings: Miami > Orlando > Tampa > Jacksonville. Jacksonville is currently the lowest performing location.

<img width="485" height="362" alt="image" src="https://github.com/user-attachments/assets/51467bd6-a340-4ca0-9863-5c079a2f7808" />

## Customer Demographics:
- Overall: The customer base is evenly split between Males (49%) and Females (51%), as well as between Singles (50%) and Families (50%).
- Weekly Trends: There is a distinct shift on weekends. Families become the dominant shopper group on Saturdays and Sundays, whereas singles are more prevalent during weekdays.

<img width="982" height="297" alt="image" src="https://github.com/user-attachments/assets/4d47ea6e-aa26-4ca2-9057-19bf6ca074f1" />

## Seasonality:
- Peak Season: Sales peak during the hot summer months (Q3) and the holiday season (December).
- Slow Season: The Spring months (specifically Q2/April) represent the lowest sales period of the year.

<img width="568" height="500" alt="image" src="https://github.com/user-attachments/assets/bd8ecca2-7568-4725-b01e-0963b835f0cf" />

### Recommendations
Based on the analysis, the following actions are recommended to improve profitability and efficiency:

Dynamic Staffing: Implement a flexible staffing schedule that reduces headcount during predicted rainy days and the slow Q2 season to control costs.

Targeted Marketing: Launch "Family Weekend" promotions to capitalize on the increased family traffic on Saturdays and Sundays. Conversely, target singles with "Happy Hour" or weekday-specific deals.

Inventory Planning: Increase stock levels significantly in preparation for the Q3 Summer rush and Q4 Holiday season to prevent stockouts; reduce inventory holding during April.

Strategic Focus: Double down on the Miami location as the primary revenue driver. For Jacksonville, investigate the root cause of low performance and test a local loyalty program to boost retention.


### Acknowledgement:

This project was completed as part of a tutorial. I want to give full credit to the original creator.

* **Author:** [[Absent Data](https://www.youtube.com/@absentdata)]
* **Tutorial:** [[Tutorial Link](https://www.youtube.com/watch?v=Hh5-Y_6v5iU&list=PLi5spBcf0UMXfbMt1X2bHQkk7mHXkTUhs&index=9)]

My goal in completing this project was to familiarize myself with MySQL, PowerBI, and GitHub.




