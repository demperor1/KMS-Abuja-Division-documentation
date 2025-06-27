# Sales-Customer-Analysis-2009-2012
## Project Overview
This analysis project focuses on the Abuja division, 
using historical order data from 2009 to 2012. The purpose of this project is to 
support the business in making data-driven decisions for improving sales performance, 
customer engagement, and shipping cost efficiency. 

## Data Source
The primary dataset used for this analysis is the sales and customer data **csv file** 
containing detailed information about sales made by company.

## Tools & Skills Used
- Ms Excel (for data cleaning)
- SQL server (for data analysis)

## Data Cleaning and Preparation
- Data loading and inspection
- Handling missing variable
- Data cleaning and formatting

## Exploratory Data Analysis
1. Which product category had the highest sales?
2. What are the top 3 and bottom 3 regions in terms of sales?
3. What were the total sales of appliances in Ontario?
4. Advise KMS on how to increase revenue from the bottom 10 customers
5. Which shipping method incurred the most cost?**
6. Who are the most valuable customers, and what do they typically buy?
7. Which small business customer had the highest sales?
8. Which corporate customer placed the most orders (2009–2012)?
9. Which consumer customer was the most profitable?
10. Who returned items and which segment do they belong to?
11. Was shipping cost appropriately spent based on order priority?

Data Analysis
This involved writing code used in analysis:

```SQL
select * from KMS_store

-----Highest sale by product category
select product_category, sum(sales) as highestsales 
from KMS_store
group by product_category
order by highestsales desc

---total sale by each region
select Region, Sum(sales) as totalsales
from KMS_store
group by Region
order by totalsales desc 

----top 3 sales by region
select top 3 Region, Sum(sales) as top3sales
from KMS_store
group by Region
order by top3sales desc 

---last 3 sales by region
select top 3 Region, Sum(sales) as last3sales
from KMS_store
group by Region
order by last3sales asc

---total sales in Ontario
select Region, sum(sales) as totalsale
from KMS_Store
where region = 'Ontario'
group by region

-----shipping mode
select Ship_mode, sum(Shipping_cost) as cost
from KMS_Store
group by ship_mode
order by cost desc

----valuable or Top 1 customer by sales
SELECT TOP 1 customer_name, product_category, SUM(sales) AS total_sales
FROM KMS_Store
GROUP BY customer_name, product_category

----valuable or Top 1 customer by profit
SELECT TOP 1 customer_name, product_category,SUM(profit) AS total_profit
FROM KMS_Store
GROUP BY customer_name, product_category
ORDER BY total_profit DESC;

---valuable or Top 1 customer by order
SELECT TOP 1 customer_name,product_category, COUNT(order_id) AS total_orders
FROM KMS_Store
GROUP BY customer_name, product_category
ORDER BY total_orders DESC;

--- the most valuable constomer
SELECT top 3 customer_name, product_category,
       SUM(sales) AS total_sales,
       SUM(profit) AS total_profit,
       COUNT(order_id) AS total_orders
FROM KMS_Store
GROUP BY customer_name,product_category
ORDER BY total_sales DESC;

----highest sales by small business customer
select  top 1 customer_name, customer_segment, sum(sales) as totalsale
from KMS_store
where customer_segment = 'small business'
group by customer_name, customer_segment
order by totalsale desc

------- highest order by corporate customer
select top 1 customer_name, customer_segment, count(order_quantity) as totalorder
from KMS_store
where customer_segment = 'corporate'
group by customer_name, customer_segment

---- highest profitable by consumer customer
select top 1 customer_name, customer_segment, sum(profit) as highestprofit
from KMS_store
where customer_segment = 'consumer'
group by customer_name, customer_segment

---shipping priority
SELECT order_priority, ship_mode, COUNT(*) AS total_orders, SUM(shipping_cost) AS total_shipping_cost
FROM KMS_Store
GROUP BY order_priority, ship_mode
ORDER BY order_priority, ship_mode desc

```

