#Pizza Sales Dashboard

### Dashboard Link : https://app.powerbi.com/links/NdUHRVdcWx?ctid=45da90b5-5f90-4348-a35c-996e9bc395d4&pbi_source=linkShare&bookmarkGuid=c20b7c5b-da4c-48c7-8fc0-ab5b6825191f

## Problem Statement

        KPI's Requirement 
we need tto analyze key indicators for our pizza sales data to gain insights innto our business performance. Specifically, we want to calculate the following metrics:
1. Total Revenue:The sum of the total price of all pizza orders.
2. Avergae Order Value: The average amount spent per order, calculate by dividing the total revenue by the total number of orders.
3. Total Pizzas Sold: The sum of the quantities of all pizza sold.
4. Total Orders: The total numbers of orders placed.
5. Average Pizzas Per Order: The average number of pizzas sold per order, calculated by dividing the total number of pizzas sold by the total number of orders.

        Charts Requirement
We would like to visualize various aspects of our pizza sales data to agin innsights and understand key trends. We have identified the following requirements for creating charts:
1. Daily trend for Total Orders:
Create a bar chart that displays the daily trend of total order over a specific time period. This chart will help us identify any patterns or fluctuations in order volumes on a daily basis.

2. Monthly Trend for Total Orders:
Create a line chart that illustrates the hourly trend of total orders throughout the day. This chart will allow us to in=dentify peak hours or periods of high order activity.

3. Percentage of Sales by pizza category:
Create a pie chart that shoes the distribution of sales across differrent pizza categories. This chart will provide insights into the popularity of various pizza categories and their contributes to overall sales. 

4. Percentage of sales by Pizza size:
Generate a pie chart that represents the percentage of sales attribubted to different pizza pizes. This chart will help us undersstan customer preferences for pizza sizes and their mpact on sales.

5. Total Pizzas sold by Pizza Category:
Create a funnel chart that presentss the total number of pizzas sold for each pizza category. This chart will allow us to compare the sales performance of different pizza categories.

6. Top 5 Best Sellers by Revenue, Total Quantity and Total Orders
Create a bar chart highlighting the top 5 best-selling pizzas based on the Revenue. Total Quantity, Total Orders. This chart will hlp us identify the most popular pizza options.

7. Bottom 5 Best Sellers by Revenue, Total Quantity and Total Orders
Create a bar chart showcsing the bottom % worst-selling piizzas based on the Revenue, Total Quantity, Total Orders. This chart will enable us to identify underperforming or less population pizza options.


### Steps followed 
#### PART 1: MS SQL SERVER
- Step 1: Import data 
- Step 2: Creating Database
- Step 3: Writing Queries
- Step 4: Creating report
#### PART 2: POWER BI
- Step 1: Connecting to MS SQL SERVER
- Step 2: Data cleaning
- Step 3: Data processing
- STep 4: Data visualizations   

By using the data the queries written are as follows:
#### A. KPIs
-       SELECT SUM(total_price) AS Total_revenue from Pizza_sales
  
![Query1](https://github.com/user-attachments/assets/5d9740cf-60ed-4fa8-a1ea-83d4c65f4c15)

-       SELECT SUM(total_price)/COUNT(DISTINCT order_id) AS Avg_order_val from Pizza_Sales 

![Query 2](https://github.com/user-attachments/assets/5de154ff-ea61-4d4a-a7c8-54d504508378)

-       SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sales

![Query 3](https://github.com/user-attachments/assets/c2ef41f5-1d66-424c-8f56-8101b622fa54)

-       SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales

![Query 4](https://github.com/user-attachments/assets/9071ac46-1155-4177-99df-afde49be4996)

-       SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / 
        CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2))
        AS Avg_Pizzas_per_order
        FROM pizza_sales

![Query 5](https://github.com/user-attachments/assets/1e63644c-788f-4a8c-8ecf-44e752f15319)

##### B. Daily Trend for Total Orders
-       SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders 
        FROM pizza_sales
        GROUP BY DATENAME(DW, order_date)
![QueryB1](https://github.com/user-attachments/assets/1d57af58-8f75-4405-8255-f3ab6806954e)

C. Monthly Trend for Orders
-       SELECT DATENAME(MONTH, order_date) as Month_Name, COUNT(DISTINCT order_id) as Total_Orders
        from pizza_sales
        GROUP BY DATENAME(MONTH, order_date)
![QueryC](https://github.com/user-attachments/assets/e0b41439-ef55-4efe-9e21-221314f9bb49)

D. % of Sales by Pizza Category
-       SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
        CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
        FROM pizza_sales
        GROUP BY pizza_category
![QueryD](https://github.com/user-attachments/assets/83dd6065-bc5a-499e-9384-dc4f7b58e904)

E. % of Sales by Pizza Size
-       SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
        CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from    
        pizza_sales) AS DECIMAL(10,2)) AS PCT
        FROM pizza_sales
        GROUP BY pizza_size
        ORDER BY pizza_size
![QueryE](https://github.com/user-attachments/assets/95eb27d3-6a1a-4e1d-b40c-ccdc21abcf74)

F. Total Pizzas Sold by Pizza Category
-       SELECT pizza_category, SUM(quantity) as Total_Quantity_Sold
        FROM pizza_sales
        WHERE MONTH(order_date) = 2
        GROUP BY pizza_category
        ORDER BY Total_Quantity_Sold DESC
![QueryF](https://github.com/user-attachments/assets/971932ae-a18b-4033-8838-fd58394a824f)

G. Top 5 Pizzas by Revenue
-       SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
        FROM pizza_sales
        GROUP BY pizza_name
        ORDER BY Total_Revenue DESC
![QueryG](https://github.com/user-attachments/assets/8c97745d-db75-4564-b402-8a31f2443218)

H. Bottom 5 Pizzas by Revenue
-       SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
        FROM pizza_sales
        GROUP BY pizza_name
        ORDER BY Total_Revenue ASC
![QueryH](https://github.com/user-attachments/assets/9e885eff-f950-480e-a9b8-3a5bc184ac8d)

I. Top 5 Pizzas by Quantity
-       SELECT Top 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
        FROM pizza_sales
        GROUP BY pizza_name
        ORDER BY Total_Pizza_Sold DESC
![QueryI](https://github.com/user-attachments/assets/0673cedf-201c-4a43-bd76-1df2ccf9e529)


J. Bottom 5 Pizzas by Quantity
-       SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
        FROM pizza_sales
        GROUP BY pizza_name
        ORDER BY Total_Pizza_Sold ASC
![QueryJ](https://github.com/user-attachments/assets/bd005fad-c108-4bd7-8d9d-89674c5ac649)

K. Top 5 Pizzas by Total Orders
-       SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
        FROM pizza_sales
        GROUP BY pizza_name
        ORDER BY Total_Orders DESC
![QueryK](https://github.com/user-attachments/assets/7b1231c7-1487-4217-8ddb-b1f08d728e4a)

L. Borrom 5 Pizzas by Total Orders
-       SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
        FROM pizza_sales
        GROUP BY pizza_name
        ORDER BY Total_Orders ASC
![QueryL](https://github.com/user-attachments/assets/3259bb1b-46f5-4ac5-b6a9-602d54e331de)

NOTE: 
If you want to apply the pizza_category or pizza_size filters to the above queries you can use  WHERE clause. Follow some of below examples
SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
WHERE pizza_category = 'Classic'
GROUP BY pizza_name
ORDER BY Total_Orders ASC

## Dashboard Snapshot(Power BI DESKTOP)
#### Home Page
![Home page](https://github.com/user-attachments/assets/8e651488-b1d7-44f6-8fb3-6915e466823c)
#### Best/Worst Sellers
![Bestworstsellers](https://github.com/user-attachments/assets/278e6941-969b-4546-a414-5aa3750c26f7)

1. Overall Sales Overview:
        
        Total Revenue: $812.41K

        Average Order Value: $38.30
        
        Total Pizzas Sold: 49K
        
        Total Orders: 21K
        
        Average Pizzas per Order: 2.32
2. Best Sellers:
        
        Top Pizza by Revenue:

        The Thai Chicken Pizza contributes the most to the revenue ($43K).
        
        Top Pizza by Quantity:

        The Classic Deluxe Pizza sold the highest quantity (2.4K pizzas).
        
        Top Pizza by Total Orders:
        
        The Classic Deluxe Pizza also leads in total orders (2.3K orders).
3. Worst Sellers:
        
        Pizza with Lowest Revenue:
        
        The Brie Carre contributes the least to the revenue ($12K).
        
        Pizza with Lowest Quantity Sold:
        
        The Brie Carre sold the least number of pizzas (490 pizzas).
        
        Pizza with Lowest Total Orders:
        
        The Brie Carre also has the lowest total orders (480 orders).
4. Sales Performance:
        Category Performance:
        
        Classical Pizzas contribute the most to total sales and orders.
        
        Size Performance:
        
        Large-sized pizzas contribute the most to the overall revenue, making up 45.84% of total sales.
        
        Small-sized pizzas have the lowest contribution (1.73%).
5. Pizza Sales by Category:

        Classical Pizzas: 14,785 pizzas sold, leading in sales.

        Supreme Pizzas: 11,903 pizzas sold.

        Chicken Pizzas: 10,892 pizzas sold.
        
        Veggie Pizzas: 11,577 pizzas sold.
6. Daily Sales Insights:

        Busiest Days:
        
        Sales peak on Fridays and Saturdays with Friday being the highest (3.5K orders).
        
        Monthly Trends:
        
        July sees the highest number of orders (3.5K orders).
        
        January also experiences high sales (3.2K orders).
        
        September and October have the lowest sales, indicating a potential off-season.
7. Additional Insights:
        
        Orders are consistently higher on weekends, specifically Friday and Saturday evenings.
        
        There’s a noticeable drop in sales in September and October, which could be explored further to understand the reasons behind this trend.
