---
layout: post
title: "SQL SELECT sum with nested selects"
description: " "
date: 2023-09-23
tags: []
comments: true
share: true
---

When working with SQL, there may be occasions when you need to calculate the sum of a column based on the results of a nested SELECT statement. This can be achieved by combining the SUM function with a subquery. In this blog post, we will explore how to use nested SELECT statements to calculate the sum in SQL.

## The Scenario

Let's consider a scenario where you have two tables: `orders` and `order_items`. The `orders` table contains information about each order, while the `order_items` table contains details about the items within each order. Each order can have multiple items associated with it.

## Example Tables

### orders

| order_id | customer_id | total_amount |
|----------|-------------|--------------|
| 1        | 1001        | 150.00       |
| 2        | 1002        | 75.50        |
| 3        | 1001        | 200.00       |

### order_items

| order_item_id | order_id | product_id | quantity |
|---------------|----------|------------|----------|
| 1             | 1        | 101        | 2        |
| 2             | 1        | 102        | 3        |
| 3             | 2        | 101        | 1        |
| 4             | 3        | 103        | 4        |

## Calculating the Sum with Nested SELECTs

To calculate the sum of the total amount for each customer, we can use nested SELECT statements. Here's an example query to achieve this:

```sql
SELECT customer_id, (SELECT SUM(total_amount) FROM orders WHERE customer_id = o.customer_id) AS total_sum
FROM orders o
GROUP BY customer_id;
```

In the above query, we are using a subquery `(SELECT SUM(total_amount) FROM orders WHERE customer_id = o.customer_id)` within the SELECT clause to calculate the sum of the total_amount for each customer. The outer query groups the results by `customer_id`.

## Output

The output of the above query will be:

| customer_id | total_sum |
|-------------|-----------|
| 1001        | 350.00    |
| 1002        | 75.50     |

This result shows the total sum of the `total_amount` column for each customer.

## Conclusion

By using nested SELECT statements, you can easily calculate the sum of a column based on the results of a subquery in SQL. This can be particularly useful when you need to perform calculations based on different conditions or groupings.