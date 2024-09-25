
# Pizza Orders SQL Queries

This document contains SQL queries for analyzing pizza orders in the database.

| Question                                                                          | SQL Query                                                                                                                            |
|-----------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| **1. What is the total number of orders placed?**                                | ```sql SELECT COUNT(order_id) AS total_orders FROM orders; ```                                                                       |
| **2. How much total revenue has been generated from pizza sales?**               | ```sql SELECT ROUND(SUM(order_details.quantity * pizzas.price), 2) AS total_sales FROM order_details JOIN pizzas ON pizzas.pizza_id = order_details.pizza_id; ``` |
| **3. What is the highest-priced pizza?**                                         | ```sql SELECT pizza_types.name, pizzas.price FROM pizza_types JOIN pizzas ON pizza_types.pizza_type_id = pizzas.pizza_type_id ORDER BY pizzas.price DESC LIMIT 1; ``` |
| **4. What is the most common pizza size ordered?**                               | ```sql SELECT pizzas.size, COUNT(order_details.order_id) AS order_count FROM pizzas JOIN order_details ON pizzas.pizza_id = order_details.pizza_id GROUP BY pizzas.size ORDER BY order_count DESC; ``` |
| **5. Which are the top 5 most ordered pizza types along with their quantities?** | ```sql SELECT pizza_types.name, SUM(order_details.quantity) AS quantity FROM pizza_types JOIN pizzas ON pizza_types.pizza_type_id = pizzas.pizza_type_id JOIN order_details ON order_details.pizza_id = pizzas.pizza_id GROUP BY pizza_types.name ORDER BY quantity DESC LIMIT 5; ``` |
| **6. What is the distribution of orders by hour of the day?**                    | ```sql SELECT HOUR(order_time) AS order_hour, COUNT(order_id) AS order_count FROM orders GROUP BY order_hour; ```                 |
| **7. How many pizzas are there in each category?**                               | ```sql SELECT category, COUNT(name) FROM pizza_types GROUP BY category; ```                                                         |
| **8. What are the top 3 most ordered pizza types based on revenue?**            | ```sql SELECT pizza_types.name, SUM(order_details.quantity * pizzas.price) AS revenue FROM pizza_types JOIN pizzas ON pizzas.pizza_type_id = pizza_types.pizza_type_id JOIN order_details ON order_details.pizza_id = pizzas.pizza_id GROUP BY pizza_types.name ORDER BY revenue DESC LIMIT 3; ``` |












































