
# Pizza Orders SQL Queries

This repository contains SQL queries for analyzing pizza orders in the Pizzahut database.

# Pizza Orders SQL Queries

This repository contains SQL queries for analyzing pizza orders.

## Queries

- Total number of orders
- Total revenue from pizza sales
- Highest-priced pizza
- Most common pizza sizes
- Top 5 ordered pizza types
- Distribution of orders by hour
- Category-wise distribution of pizzas
- Top 3 pizza types based on revenue




### 1. What is the total number of orders placed?
```sql
SELECT COUNT(order_id) AS total_orders FROM orders;


    
