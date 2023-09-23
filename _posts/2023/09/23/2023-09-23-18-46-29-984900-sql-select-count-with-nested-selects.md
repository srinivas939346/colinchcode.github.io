---
layout: post
title: "SQL SELECT count with nested selects"
description: " "
date: 2023-09-23
tags: []
comments: true
share: true
---

Nested selects, also known as subqueries, are used when you want to perform a query within another query. This can be useful when you need to retrieve data based on certain conditions from another table.

To illustrate how to use a nested select with `COUNT()`, let's assume we have two tables: `orders` and `customers`. The `orders` table contains information about orders placed by customers, while the `customers` table contains information about the customers themselves. We want to find the number of orders placed by customers in a specific city.

Here's an example SQL query that accomplishes this:

```sql
SELECT COUNT(*) FROM orders
WHERE customer_id IN (SELECT customer_id FROM customers WHERE city = 'New York');
```

In this example, the subquery `(SELECT customer_id FROM customers WHERE city = 'New York')` retrieves the customer IDs of customers who are located in New York. The outer query then uses this list of customer IDs to count the number of orders placed by customers in New York.

Make sure to replace `'New York'` with the desired city name in the condition to get the count for a different city.

Using this nested `SELECT` with `COUNT` allows you to perform more complex queries and retrieve specific aggregated results based on your requirements.