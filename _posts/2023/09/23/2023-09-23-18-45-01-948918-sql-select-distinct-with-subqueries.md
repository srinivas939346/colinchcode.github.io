---
layout: post
title: "SQL SELECT distinct with subqueries"
description: " "
date: 2023-09-23
tags: [SELECT, distinct]
comments: true
share: true
---

In SQL, the `SELECT DISTINCT` statement is used to retrieve only distinct (unique) values from a table. This is useful when you want to eliminate duplicate rows from the result set.

Subqueries, on the other hand, are queries that are nested within another query. They can be used to perform complex calculations or retrieve specific data based on certain conditions.

In some cases, you may need to use a subquery with the `SELECT DISTINCT` statement to get unique values from a subquery result. Let's see how this can be done with an example.

## Example:

Consider a database with two tables - `customers` and `orders`. The `customers` table contains information about the customers, and the `orders` table contains information about the orders placed by the customers. 

Suppose we want to retrieve a list of unique customer names who have placed orders. We can achieve this by using a subquery along with the `SELECT DISTINCT` statement as follows:

```sql
SELECT DISTINCT customer_name
FROM customers
WHERE customer_id IN (SELECT DISTINCT customer_id FROM orders);
```

In the above example, the inner subquery `(SELECT DISTINCT customer_id FROM orders)` retrieves all the unique customer IDs from the `orders` table. The outer query then uses these customer IDs to retrieve the corresponding distinct customer names from the `customers` table.

## Conclusion:

Using the `SELECT DISTINCT` statement with subqueries allows you to filter out duplicate values from a table based on specific conditions. This can be handy when you need to retrieve unique data from a related table.

Remember, subqueries can be nested within other queries to perform more complex operations. Experiment with different subquery conditions and explore the power of SQL in retrieving unique values efficiently.

#SQL #SELECT #distinct #subqueries