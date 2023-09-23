---
layout: post
title: "SQL SELECT aggregate with having"
description: " "
date: 2023-09-23
tags: [AggregateFunctions]
comments: true
share: true
---

Let's take a look at an example to understand how to use the `SELECT` statement with an aggregate function and the `HAVING` clause.

Suppose we have a table called `Orders` with the following columns:

- `OrderID` (primary key)
- `CustomerID`
- `OrderAmount`

Now, let's say we want to find the customers who have placed orders with a total amount greater than $1000.

Here's how we can achieve this using the `SELECT`, `SUM`, and `HAVING` clauses in SQL:

```sql
SELECT CustomerID, SUM(OrderAmount) AS TotalAmount
FROM Orders
GROUP BY CustomerID
HAVING SUM(OrderAmount) > 1000;
```

In the above example, we first select the `CustomerID` and calculate the sum of `OrderAmount` for each customer using the `SUM` function. We also give this calculated sum a column alias `TotalAmount`.

Next, we group the result by `CustomerID` using the `GROUP BY` clause. This ensures that the aggregate function operates on each group separately.

Finally, we use the `HAVING` clause to filter the results based on the condition that the sum of `OrderAmount` should be greater than 1000.

By executing this query, we will retrieve the `CustomerID` and the total order amount for customers who have placed orders with a sum greater than $1000.

Remember, the `HAVING` clause is used specifically for filtering based on aggregate functions, while the `WHERE` clause is used for applying conditions to individual rows of data.

#SQL #AggregateFunctions