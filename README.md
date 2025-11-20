# Adventure Works - Sales Performance Dashboard
## Project Overview

This capstone project involves the development of an end to end sales performance dashboard for Adventure Works. The goal was to transform raw sales data into a dynamic, interactive tool to provide actionable insights. The dashboard answers key questions about sales, profit, product performance, and regional trends, enabling data driven decision making.

## Problem Statement
The Adventure Works sales team lacked a centralized, real time view of their performance. And couldn't easily:
* Track key performance indicators (KPIs) like Sales, Profit, and Year over Year Growth.

* Identify top performing products, regions, and salespeople.

* Analyze sales trends over time to understand seasonality and performance against the previous year.

The objective was to build a comprehensive dashboard to solve these problems 

## ETL Process
Data was loaded and transformed in the Power Query Editor.
* Data Cleaning: Checked and standardized data types across all tables 
* Normalization: The data was structured into dimension and fact tables.
* Date Table: A dedicated Date table was created using DAX to support time intelligence calculations.

##  Data Modeling (Star Schema)
A data model was built following star schema best practices to ensure optimal performance and ease of analysis.
* Fact Table: Sales (containing quantitative data like Sales, Cost, Quantity)
* Dimension Tables: Product, Region, Salesperson, and Date (containing descriptive attributes)
* Relationships: All dimensions are joined to the Sales fact table on a one-to-many (*:1) cardinality, flowing filters from dimensions to the fact table.

## Schema
 <img width="1507" height="738" alt="Schema diagram" src="https://github.com/user-attachments/assets/e7190097-8ea6-4d93-834e-d40d51187c8c" />

## DAX Measures
DAX was used to create all calculations for the dashboard. 
* Total_sales = SUM(Sales[Sales])
* Total_profit = SUMX(Sales,[Total_sales]-[Total_cost])
* Profit_margin % = DIVIDE([Total_profit],[Total_sales])
* Total_transacitons = COUNTROWS(Sales)
* AVG_sale_value = DIVIDE([Total_sales],[Total_transacitons])
* Sales YTD = TOTALYTD([Total_sales],'Date'[Date])
* Sales_last_year = CALCULATE(SUM(Sales[Sales]),SAMEPERIODLASTYEAR('Date'[Date]))
* Sales YOY % = DIVIDE(([Total_sales]-Sales[Sales_last_year]),Sales[Sales_last_year])

## Dashboard Design & Visualizations
A custom theme was created using the official Adventure Works logo colors to ensure professional branding.
* KPI Cards: Total Sales, Total Profit, Profit Margin %, Sales YoY %. These provide an instant snapshot of business health.
* Line and Column Chart (Total sales and Sales last year by Month): Visually compares the current year's performance (columns) against the previous year (sales) to easily spot trends and seasonality.
* Bar Chart (Total sales by Region): Identifies top performing regions.
* Scatter Plot for Total sales, AVG sale value and Quantity sold by Salesperson.
* Slicers (Year, Country): Allow for dynamic filtering of the entire report.

<img width="1375" height="776" alt="Screenshot 2025-11-20 190442" src="https://github.com/user-attachments/assets/11825933-cf87-4964-adc2-7bc52e1f26d2" />


