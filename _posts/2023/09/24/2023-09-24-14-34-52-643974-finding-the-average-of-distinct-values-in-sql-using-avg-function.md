---
layout: post
title: "Finding the average of distinct values in SQL using AVG function"
description: " "
date: 2023-09-24
tags: [average]
comments: true
share: true
---

In SQL, the AVG function is commonly used to calculate the average value of a column in a table. However, if the column contains duplicate values, the AVG function will consider all the occurrences of each value when calculating the average. 

To calculate the average of distinct values in SQL, we can make use of the DISTINCT keyword along with the AVG function. Here's an example:

```sql
SELECT AVG(DISTINCT column_name)
FROM table_name;
```
Replace `column_name` with the name of the column you want to calculate the average of, and `table_name` with the name of the table where the column resides.

For instance, let's assume we have a table called "sales" with two columns: "product" and "sales_amount". We can find the average sales amount for distinct products using the following query:

```sql
SELECT AVG(DISTINCT sales_amount)
FROM sales;
```

This query will calculate the average sales amount considering only the distinct values in the "sales_amount" column.

Using the AVG function along with the DISTINCT keyword allows us to find the average of distinct values in SQL. By understanding and utilizing this capability, you can obtain accurate averages in scenarios where duplications exist in the data.

#sql #average