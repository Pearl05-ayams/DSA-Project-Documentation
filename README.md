# DSA Project Documentation - Kultra Mega Stores Inventory (SQL)
## Introduction 
As a privileged trainee of DSA training on Data Analysis, I have been given the opportunity to have a hands-on experience which is valuable for reinforcing your learning and gaining real-world experience. 
## Project Overview 
The analysis of Kultra Mega Stores' order (2009-2012) data offers valuable insights that can help inform business decisions, drive growth, and improve operations by understanding customer behavior, sales patterns, and product demand.
## Project Data Source
CSV files 
## Data Tool Used
SQL Server: 
1. Data extraction from data source
2. Data Transformation by imputation of the right data types for analysis 
3. Query and Analysis
## Analysis
[Uploading dsa project - Kultra Mecreate database [Kultra_Mega_Stores_db]


--import files--


select * from kms_file

select * from kms_file
alter table  kms_file
alter column sales decimal (10,2)
alter table  kms_file
alter column discount decimal (10,2)
alter table  kms_file
alter column sales decimal (10,2)
alter table  kms_file
alter column profit decimal (10,2)
alter table  kms_file
alter column unit_price decimal (10,2)
alter table kms_file
alter column shipping_cost decimal (10,2)
alter table kms_file
alter column product_base_margin decimal (10,2)


select * from kms_file
-----SCENARIO 0NE----
---1. Which product category had the highest sales?
select top 1 Product_Category, sum(Sales) as highest_Sales from kms_file
Group by Product_Category
ORDER BY highest_Sales desc

--2. What are the Top 3 and Bottom 3 regions in terms of sales?
--(3 top regions)
select top 3 Region, sum(sales) as most_profitableRegion from kms_file
GROUP BY Region
order by most_profitableRegion desc
--(3 bottom regions)
select top 3 Region, sum(sales) as most_profitableRegion from kms_file
GROUP BY region
order by most_profitableRegion asc

---3.What were the total sales of appliances in Ontario? 
 select sum(sales) as total_sales from kms_file
WHERE province = 'ontario' and product_sub_category = 'appliances'

--4.Advise the management of KMS on what to do to increase the revenue from the bottom 10 customers
 SELECT TOP 10 order_ID, product_name, SUM(sales) AS total_revenue
FROM (select order_id, sales, product_name from kms_file) as order_id
GROUP BY Order_ID, Product_Name
ORDER BY total_revenue ASC
---purchase range between 2.24-4.94 falls in a category of low cost office supplies. this could be due to infrequent orders by the customers. in order to increase revenue, there has to be reduction of cost on product also product building to move slower selling items in the market.

-- 5. KMS incurred the most shipping cost using which shipping method?
     SELECT ship_mode, SUM(Shipping_Cost) AS TotalCost
FROM kms_file
GROUP BY Ship_Mode
ORDER BY TotalCost DESC

---SCENARIO TWO---
--6. Who are the most valuable Customers, and what products or services do they typically purchase?
Select Top 1 Customer_Segment, Product_Sub_Category, Sum(Unit_Price*Order_Quantity*(1-Discount)) as Total_Revenue from kms_file
Group by Customer_Segment, Product_Sub_Category
order by Total_Revenue desc

---7. Which small business customer had the highest sales?
select top 1 Customer_Name, sum(sales) as highest_Sales from kms_file
where Customer_Segment = 'Small Business'
Group by Customer_Name
ORDER BY  highest_Sales desc

---8. Which Corporate Customer placed the most number of orders in 2009 � 2012? 
select top 1 customer_name, count(order_id) as total_order
from kms_file
where Customer_Segment = 'corporate'
group by Customer_Name
order by total_order desc

---9. Which consumer customer was the most profitable one? 
select top 1 customer_name, sum(sales) as mostProfitable from kms_file
where customer_segment = 'consumer'
group by Customer_Name
order by mostProfitable desc
select * from kms_file
--10. Which customer returned items, and what segment do they belong to? 
select customer_name, customer_segment, profit from kms_file
where profit < 0 or Sales < = 0
--Ans: Negative profit is an indicator of returned item; because of money loss 
---Import files--
---drop table [dbo].[Order_Status]
select * from return_status
select * from kms_file
---10. Which customer returned items, and what segment do they belong to?
select distinct kms_file.order_id, kms_file.customer_name, kms_file.customer_segment
from kms_file
join return_status
on kms_file.order_id = return_status.order_id
where [status] = 'returned' 



--11. Do you think the company appropriately spent shipping costs based on the Order Priority? Explain your answer 


select Order_Priority, ship_mode, count(order_id) as order_count, 
avg("Shipping_Cost") as avg_ship_cost
from kms_file
group by order_priority, Ship_Mode
order by Order_Priority, avg_ship_cost

---Ans: Shipping cost was based on priority. Delivey truck had more responce to order from critical to not specified. ga Stores Inventory - Copy.sql…]()


