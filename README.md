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
create database KMS

select * from KMS_store

alter table KMS_Store
alter column profit decimal (10,2)

-----Highest sale by product category
select top 1 product_category, sum(sales) as highestsales 
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

select * from KMS_store

---total sales in Ontario
select Region, sum(sales) as totalsale
from KMS_Store
where region = 'Ontario'
group by region

---total sale by 10 bottom customer
select top 10 customer_name, sum(sales) as revenue 
from KMS_Store
group by customer_name
order by revenue asc

-----total shipping cost
select Ship_mode, sum(Shipping_cost) as total_cost
from KMS_Store
group by ship_mode
order by total_cost desc

select * from KMS_store

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


select * from KMS_store

---- highest profitable by consumer customer
select top 1 customer_name, customer_segment, sum(profit) as highestprofit
from KMS_store
where customer_segment = 'consumer'
group by customer_name, customer_segment


---order of priority
select order_priority, ship_mode, count(order_id) as total_order,
round(sum(sales - profit),2) as estimated_shipping_cost, 
Avg(DATEDIFF (DAY, [order_date], [ship_date])) as Avg_shipping_days
from KMS_store
group by order_priority, ship_mode
order by total_order desc
	
	
	/* Analyzing the shipping modes used for different order priorities, 
	the result showed that some low-priority orders were shipped via Express Air, 
	which is the fastest and most expensive option and high 
	or critical priority orders was used via Delivery Truck, the slowest and cheapest method. 
	This suggests the company did not consistently align shipping methods with order of priority, 
	potentially leading to unnecessary costs or delayed deliveries for important orders.*/
```
## Result and finding
The Analysis results are sumarised as follow:
- The Furniture category had the highest sales.
- The East region had the lowest sales.
- Corporate clients generated the highest sales volume.
- Delivery truck incurred the most shipping cost.

## Recommendations
1. Focus more marketing on Furniture and Appliances
2. Re-engage low-spending customers via loyalty incentives
3. Align shipping method with order priority to cut costs
4. Investigate and resolve high return rates in specific categories
5. Offer exclusive deals to high-value customers (especially corporate)
6. Regional marketing efforts should be focused on improving sales in the bottom regions through localized promotions or outreach.
7. Profitable customers should be prioritized for early product launches and reward programs.

## Conclusion
This analysis of Kultra Mega Stores’ (KMS) order data from 2009 to 2012 has provided 
valuable insights into product performance, regional sales trends, customer behavior, 
and operational efficiency. By leveraging SQL queries and structured exploration, 
we identified key areas of strength—such as high-performing product categories 
(e.g., Furniture), loyal corporate customers, and high sales regions (West, Central, Ontario).
We also uncovered inefficiencies, such as misaligned shipping costs and order priorities, 
underperforming regions, and customers with low engagement. In particular, 
the use of Express Air for low-priority orders represents a significant cost-saving
opportunity. Additionally, identifying the most profitable and loyal customers presents 
an opportunity to implement targeted marketing and retention strategies.
