---
layout: post
title: "Using SQL AVG with partitioning or window functions"
description: " "
date: 2023-09-24
tags: []
comments: true
share: true
---

In SQL, the `AVG` function is commonly used to calculate the average of a set of values in a column. However, when working with more complex data, such as when you want to calculate the average per group or within a specific range, you can leverage partitioning or window functions to achieve the desired results.

### Partitioning with AVG

Partitioning refers to dividing the data into groups based on a specific column. By using the `PARTITION BY` clause with the `AVG` function, you can calculate the average for each partition separately, resulting in more granular averages.

Consider a table `sales` with the following structure:

```sql
CREATE TABLE sales (
    product_id INT,
    sales_date DATE,
    amount DECIMAL(10, 2)
);
```

To calculate the average sales amount per product, you can use the `PARTITION BY` clause like this:

```sql
SELECT product_id, AVG(amount) OVER (PARTITION BY product_id) AS average_sales
FROM sales;
```

This query will partition the data by `product_id` and compute the average `amount` for each partition, resulting in a list of products with their corresponding average sales.

### Window Functions with AVG

Window functions allow you to perform calculations across a set of rows within a specified window. In the case of `AVG`, you can define the window using the `ROWS` or `RANGE` clauses, specifying the number of preceding or following rows or a range of values to include in the calculation.

Let's say you want to calculate the moving average of the last three sales amounts per product. You can leverage window functions like this:

```sql
SELECT product_id, AVG(amount) OVER (PARTITION BY product_id ORDER BY sales_date ROWS BETWEEN 2 PRECEDING AND CURRENT ROW) AS moving_average
FROM sales;
```

In this example, the `ORDER BY` clause ensures that the calculation considers the sales amounts in chronological order. The `ROWS BETWEEN 2 PRECEDING AND CURRENT ROW` clause defines the window as the current row and the two preceding rows. The resulting query will return the moving average for each product based on the previous three sales amounts.

By using partitioning or window functions alongside the `AVG` function, you can perform more advanced calculations depending on your specific requirements. These techniques provide flexibility and granularity in analyzing data in SQL.

#SQL #AVG