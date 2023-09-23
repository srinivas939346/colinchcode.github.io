---
layout: post
title: "SQL SELECT avg with joins"
description: " "
date: 2023-09-23
tags: [JOIN]
comments: true
share: true
---

In SQL, the `SELECT` statement allows us to retrieve data from one or more tables. Using JOIN operations, we can combine data from multiple tables based on a related column. While performing joins, it is also possible to use the `AVG` function to calculate the average of a specific column.

Let's say we have two tables - `orders` and `customers`. The `orders` table contains information about orders, including the order ID, customer ID, and order amount. The `customers` table contains customer information, with the customer ID and customer name.

To calculate the average order amount for each customer, we can join these two tables based on the customer ID and use the `AVG` function to calculate the average amount.

Here's an example SQL query that demonstrates this:

```
SELECT customers.customer_name, AVG(orders.order_amount) AS average_order_amount
FROM customers
JOIN orders ON customers.customer_id = orders.customer_id
GROUP BY customers.customer_name;
```

In the above query:
- We select the `customer_name` column from the `customers` table.
- We use the `AVG` function to calculate the average of the `order_amount` column from the `orders` table.
- We join the `customers` and `orders` tables using the `customer_id` column.
- Finally, we group the result by the `customer_name` column.

The `GROUP BY` clause is used to group the result based on the `customer_name` column so that the average calculation is applied to each customer individually.

By executing this SQL query, we can obtain the average order amount for each customer.

Using `SELECT` statement, joins, and aggregate functions like `AVG`, we can perform powerful calculations and analysis in SQL, making it an essential tool for data manipulation and data analysis tasks.

#SQL #JOIN