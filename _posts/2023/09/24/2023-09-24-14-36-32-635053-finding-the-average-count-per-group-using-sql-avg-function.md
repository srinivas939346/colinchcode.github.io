---
layout: post
title: "Finding the average count per group using SQL AVG function"
description: " "
date: 2023-09-24
tags: []
comments: true
share: true
---

Here's an example to demonstrate how to use the AVG function to find the average count per group:

```sql
SELECT group_column, AVG(count_column) AS average_count
FROM your_table
GROUP BY group_column;
```

In this example, replace `group_column` with the column name that defines your groups, and `count_column` with the column name that contains the count or quantity you want to calculate the average for. Replace `your_table` with the name of your table.

The `GROUP BY` clause groups the data by the distinct values in the `group_column`. The AVG function then calculates the average of the values in the `count_column` for each group.

For instance, let's consider a table called `sales` with columns `product` and `quantity`. We want to find the average quantity of each product sold:

```sql
SELECT product, AVG(quantity) AS average_quantity
FROM sales
GROUP BY product;
```

After executing this query, you will get the average quantity for each product in the table.

The result will be displayed with the `product` and `average_quantity` columns. The `average_quantity` column will contain the average count per group.

By using the AVG function and the GROUP BY clause, you can easily calculate the average count per group in SQL. This can be helpful for analyzing data and making informed business decisions based on average quantities or occurrences within different groups.

#SQL #AVG