### 1.Sales Performance & Revenue Analysis

## Total Revenue
select round(sum(p.price*od.quantity)) as Total_Revenue from order_details od join pizzas p on od.pizza_id=p.pizza_id ;

![image](https://github.com/user-attachments/assets/75fdc37a-a102-48b5-9260-b5c9bc003873)

## Monthly Sales Trends
SELECT DATE_FORMAT(o.date, '%Y-%m') AS month, round(SUM(p.price * od.quantity)) AS monthly_sales
FROM orders o
JOIN order_details od ON o.order_id = od.order_id
JOIN pizzas p ON od.pizza_id = p.pizza_id
GROUP BY month
ORDER BY month;

![image](https://github.com/user-attachments/assets/fb2239d5-3f9f-4d46-a9d3-b370b882066f)

## Peak Sales Hours
SELECT HOUR(o.time) AS Hour, COUNT(*) AS Order_Count
FROM orders o
JOIN order_details od ON o.order_id = od.order_id
GROUP BY hour
ORDER BY order_count DESC;

![image](https://github.com/user-attachments/assets/f0941f46-f6ba-46a7-9f0f-638a5cecc81c)

### 2.Best-Selling & Least-Selling Pizzas

## What are the top 5 best-selling pizzas?
SELECT p.pizza_id, p.size, COUNT(od.pizza_id) AS total_sold
FROM order_details od
JOIN pizzas p ON od.pizza_id = p.pizza_id
GROUP BY p.pizza_id, p.size
ORDER BY total_sold desc
LIMIT 5;

![image](https://github.com/user-attachments/assets/6e1684b6-faac-457b-9c1b-43de86913237)

## What are the top 5 Least-selling pizzas?
SELECT p.pizza_id, p.size, COUNT(od.pizza_id) AS total_sold
FROM order_details od
JOIN pizzas p ON od.pizza_id = p.pizza_id
GROUP BY p.pizza_id, p.size
ORDER BY total_sold asc
LIMIT 5;

![image](https://github.com/user-attachments/assets/eea4a2ab-6651-4609-a6db-f8695eaa3f34)

### 3.Inventory & Waste Management
## Which pizza sizes are most popular?
SELECT p.size, COUNT(od.pizza_id) AS total_sold
FROM order_details od
JOIN pizzas p ON od.pizza_id = p.pizza_id
GROUP BY p.size
ORDER BY total_sold DESC;

![image](https://github.com/user-attachments/assets/195fc74a-5b40-463c-98a1-4308945c9ef7)

## Which ingredients are used most frequently?
SELECT pt.ingredients, COUNT(od.pizza_id) AS total_sold
FROM order_details od
JOIN pizzas p ON od.pizza_id = p.pizza_id
JOIN pizza_types pt ON p.pizza_type_id = pt.pizza_type_id
GROUP BY pt.ingredients
ORDER BY total_sold DESC;

![image](https://github.com/user-attachments/assets/01300e65-3aef-4d8e-a28b-fd98d65d9b8d)


## Most Common Order Combinations
SELECT od1.pizza_id AS pizza_1, od2.pizza_id AS pizza_2, COUNT(*) AS combo_count
FROM order_details od1
JOIN order_details od2 ON od1.order_id = od2.order_id AND od1.pizza_id < od2.pizza_id
GROUP BY pizza_1, pizza_2
ORDER BY combo_count DESC
LIMIT 5;

![image](https://github.com/user-attachments/assets/c5ee72e2-7de6-4c48-8ec2-a3b749e9d7c6)









