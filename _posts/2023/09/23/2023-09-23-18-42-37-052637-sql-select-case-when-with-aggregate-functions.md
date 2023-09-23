---
layout: post
title: "SQL SELECT case when with aggregate functions"
description: " "
date: 2023-09-23
tags: [AggregateFunctions]
comments: true
share: true
---

In SQL, the `CASE WHEN` statement is used to perform conditional logic within a `SELECT` query. It allows you to define specific conditions and return different values based on those conditions. When combined with aggregate functions, such as `SUM`, `COUNT`, or `AVG`, it becomes a powerful tool for gathering useful insights from your data.

Let's see an example of how `CASE WHEN` can be used with aggregate functions:

```sql
SELECT 
    product_category,
    SUM(CASE WHEN product_price > 1000 THEN 1 ELSE 0 END) AS expensive_products,
    COUNT(CASE WHEN product_quantity < 10 THEN product_id END) AS low_stock_products,
    AVG(CASE WHEN product_rating >= 4 THEN product_rating ELSE NULL END) AS average_rating
FROM
    products
GROUP BY
    product_category;
```

In the above example, we have a table named "products" with columns like "product_category", "product_price", "product_quantity", and "product_rating". We want to gather some insights about the products based on their category and certain conditions.

- The first line of the `SELECT` statement selects the "product_category" column as it is.
- The second line uses the `SUM` function combined with a `CASE WHEN` statement. It counts the number of products whose price is greater than 1000 and returns it as "expensive_products".
- The third line uses the `COUNT` function combined with a `CASE WHEN` statement. It counts the number of products whose quantity is less than 10 and returns it as "low_stock_products".
- The fourth line uses the `AVG` function combined with a `CASE WHEN` statement. It calculates the average rating of products with a rating greater than or equal to 4, and returns it as "average_rating".

The `GROUP BY` clause groups the result by the "product_category" column, so you can see the aggregated values for each category.

This example demonstrates how you can leverage `CASE WHEN` with aggregate functions to perform conditional calculations and gather insights from your data. It can be useful in various scenarios, such as analyzing sales data, inventory management, or customer segmentation.

#SQL #AggregateFunctions