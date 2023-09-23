---
layout: post
title: "SQL SELECT max with joins"
description: " "
date: 2023-09-23
tags: []
comments: true
share: true
---

When working with SQL, it is common to use `JOIN` clauses to combine data from multiple tables. Sometimes, you may need to retrieve the maximum value from a column in one table while joining it with another table.

In this blog post, we'll explore how to use the `MAX` function in SQL along with `JOIN` clauses to accomplish this task.

## Example Scenario

Let's consider a scenario where you have two tables: `orders` and `customers`. The `orders` table contains information about the orders placed, including the customer ID (`customer_id`) and the total order amount (`order_amount`). The `customers` table contains customer details, including the customer ID (`id`) and the customer's name (`name`).

## SQL Query

To find the maximum order amount along with the corresponding customer name, you can use the following SQL query:

```sql
SELECT c.name, o.order_amount
FROM orders o
JOIN customers c ON o.customer_id = c.id
WHERE o.order_amount = (
    SELECT MAX(order_amount)
    FROM orders
)
```

Let's break down this query step by step:

1. We start by selecting the customer name (`c.name`) and order amount (`o.order_amount`) from the `orders` and `customers` tables.
2. We use the `JOIN` clause to join the `orders` and `customers` tables based on the customer ID (`o.customer_id = c.id`).
3. We then add a `WHERE` clause to filter the results based on the maximum order amount. The subquery `(SELECT MAX(order_amount) FROM orders)` retrieves the maximum order amount from the `orders` table.
4. Finally, we execute the query to retrieve the desired result.

## Conclusion

In this blog post, we've learned how to use the `MAX` function in SQL to find the maximum value from a column when using `JOIN` clauses. By combining the power of `MAX` and `JOIN`, you can easily retrieve the desired information from multiple tables.

Remember to adapt this query to match the table names and column names in your specific database schema.