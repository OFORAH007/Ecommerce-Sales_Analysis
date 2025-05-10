# Superstoresales Analysis

## Table of Content

 - [Project Overview](#project-overview)
 - [Data Sources](#data-sources)
 - [Tools](tools)
 - [Data Preparation](#data-preparation)
 - [Exploratory Data Analysis](#exploratory-data-analysis)
 - [Data Analysis](#data-analysis)
 - [Results](#results)
 - [Recommendations](#recommendations)
 - [Limitations](#limitations)
 - [References](#references)

### Project Overview

This data analysis project aims to provide insights into the sales performance of an E-commerce company over the past year. By analyzing various aspect of the sales data, We seek to identify trends , make data driven recommendations, and gain deeper understanding of Superstore's performance.

### Data Sources

Sales Data: The primary dataset used for this analysis is the "Superstore.XLSX" File, containing detailed information about each sales made by the Company.

### Tools

 - Excel - Data Cleaning [Download here](https://microsoft.com)
 - SQL Server - Data Extraction
 - Power BI - Creating Visualization and reports

### Data Preparation

In the initial data preparation phase, We performed the following tasks;
 1. Data loading and Inspection.
 2. Handling of the missing values.
 3. Removal of duplicate values.
 4. Standardization of the data.

### Exploratory Data Analysis

Exploratory Data Analysis(EDA) exploring the sales  data to answer some key questions, Like;

 - What is the overall sales trend?
 - Which products are top 5 sellers?
 - What are the peak sales period?
 - Which products sales the most in each states?

### Data Analysis

Include some interesting codes/features worked with;

 - Top 5 Product By Profit

```SQL 1 
SELECT 
    [Product Name], 
    SUM([Profit]) AS Total_Profit
FROM 
    Superstore
GROUP BY 
    [Product Name]
ORDER BY 
    Total_Profit DESC
LIMIT 5;
```

 - Monthly Sales Trends by Region

```SQL 2
SELECT 
    DATE_TRUNC('month', [Order Date]) AS Month,
    [Region],
    SUM([Sales]) AS Total_Sales
FROM 
    Superstore
GROUP BY 
    Month, [Region]
ORDER BY 
    Month, [Region];
```

 - Customer Segment with the highest return

```SQL 3
SELECT 
    [Customer Segment],
    COUNT(*) AS Total_Orders,
    SUM(CASE WHEN [Returned] = 'Yes' THEN 1 ELSE 0 END) AS Returns,
    ROUND(SUM(CASE WHEN [Returned] = 'Yes' THEN 1 ELSE 0 END) * 100.0 / COUNT(*), 2) AS Return_Rate_Percent
FROM 
    Superstore
GROUP BY 
    [Customer Segment]
ORDER BY 
    Return_Rate_Percent DESC;
```

### Results

The analysis result are summarised as follows;

1. The  Superstore's sales and profit tends to peak at Q4 (Octomber - December) due to year-end purchasing behaviour and there is a slight slump in Q1, common in retail due to post-holiday slow down.
2. High Sales does not always equal high profit. Some orders with very high sales amount results in net losses.
3. Customers Segment contributed the most in Total Sales while Corporate and Home office Segment have a better profit margin per order probably due to bulk purchases with lower operational overhead.
4. Technology is the most profitable category. Office Supplies and Furniture generates high sales but often shows lower or negative profit especially in sub-categories like Table.
5. Table is the worst performing sub-category, often shows negative profit due to high shipping cost or heavy discount.

### Recommendations

Based on the analysis, I recommend the following actions to be initaited;
 - Capitalize on Seasonal Peak - Run targetted Promotions and Ads in advance of October and Decemebr (Q4) when market sales and profit are strong.
 - Optimize Inventory for high profit items.
 - Reduce discount on unprofitable products - Avoid giving a high discount of (20%-30%) on low margin sub-categories like Tables.
 - Review the Shipping Cost and Strategies.
 - Implement a Customer Segementation strategy to target high-LTC Customers effectively.

### Limitations

 - There was no detailed breakdown on the Cost of Goods (COGs), Shipping Cost or Supplier pricing limitting margin analysis.
 - There was incomplete customers behavior data (no age, location, income and specificity)
 - It doesn't include external factors like economic trends, competitive activity, marketting campaigns which might limit real world applications.

### References

1. Data Analysis with SQL and Excel by Gordon S. Linoff (2nd Edition, Wiley)
2. Fundamentals of Business data Analytics by R.V. Ramanujam & Ramesh Sharda (Pearson)
3. [Tableau Superstore Dataset](https://www.tableau.com/learn/sample-data)




