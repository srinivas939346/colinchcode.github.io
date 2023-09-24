---
layout: post
title: "Using GROUP BY with SQL AVG function to calculate average for multiple groups"
description: " "
date: 2023-09-24
tags: [GROUPBY]
comments: true
share: true
---

In SQL, the `GROUP BY` clause is used to group rows based on one or more columns. When combined with the `AVG` function, it can be used to calculate the average for multiple groups in a table.

Let's consider a scenario where we have a `sales` table with the following columns: `product`, `category`, and `sales_amount`. We want to find the average sales amount for each category.

Here's an example query that demonstrates how to achieve this:

```sql
SELECT category, AVG(sales_amount) AS average_sales
FROM sales
GROUP BY category;
```

In the above query, we select the `category` column and use the `AVG` function to calculate the average of the `sales_amount` column. We give the resulting column an alias `average_sales`.

The `GROUP BY category` statement groups the rows based on the `category` column, which means that for each unique category, the average sales amount will be calculated.

The output of the above query will display each category along with its corresponding average sales amount.

Here's a sample result:

| category    | average_sales |
|------------ |-------------- |
| Electronics | 5000          |
| Clothing    | 3500          |
| Home        | 4000          |

In this example, we can see that the average sales amount for the `Electronics` category is 5000, for the `Clothing` category is 3500, and for the `Home` category is 4000.

By using the `GROUP BY` clause with the `AVG` function, we can easily calculate average values for multiple groups in a SQL table. This is useful for analyzing data and gaining insights from large datasets.

#SQL #AVG #GROUPBY