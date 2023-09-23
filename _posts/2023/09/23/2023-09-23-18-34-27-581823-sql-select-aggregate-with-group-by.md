---
layout: post
title: "SQL SELECT aggregate with group by"
description: " "
date: 2023-09-23
tags: [AggregateFunctions]
comments: true
share: true
---

In SQL, **aggregate functions** are used to perform calculations on a set of values and return a single value as the result. The **GROUP BY** clause is used in combination with aggregate functions to group rows based on one or more columns.

Let's say we have a table called `orders` with the following columns: `order_id`, `customer_id`, `product_id`, and `order_amount`. We want to calculate the total order amount for each customer.

Here's an example query that uses the `SUM` aggregate function with `GROUP BY`:

```sql
SELECT customer_id, SUM(order_amount) AS total_order_amount
FROM orders
GROUP BY customer_id;
```

In this query:
- We select the `customer_id` column and calculate the sum of `order_amount` for each customer.
- The result is aliased as `total_order_amount` using the `AS` keyword.
- The `GROUP BY` clause groups the rows by the `customer_id` column.

The output of this query will be a result set with two columns: `customer_id` and `total_order_amount`. Each row represents a unique customer and the total order amount for that customer.

You can also use other aggregate functions like `COUNT`, `AVG`, `MIN`, `MAX`, etc., along with `GROUP BY` to perform different calculations on grouped data.

**Note:** The columns that are not part of the `GROUP BY` clause should be used with an aggregate function or included in the `SELECT` clause as part of the grouping.

#SQL #AggregateFunctions