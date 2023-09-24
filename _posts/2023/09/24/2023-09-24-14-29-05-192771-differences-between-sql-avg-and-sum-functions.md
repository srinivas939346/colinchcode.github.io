---
layout: post
title: "Differences between SQL AVG and SUM functions"
description: " "
date: 2023-09-24
tags: [hashtags, aggregation]
comments: true
share: true
---

In SQL, the `AVG` and `SUM` functions are used to perform different calculations on numeric columns in a table. While both functions deal with aggregating values, they produce different results. Let's dive into the differences between these two functions.

## 1. AVG Function

The `AVG` function calculates the average of a set of values in a numeric column. It returns the average as a decimal or floating-point number.

The syntax for using the `AVG` function is as follows:

```sql
SELECT AVG(column_name) FROM table_name;
```

For example, suppose we have a table named `sales` with a column named `amount` that stores the sales made by each employee. To calculate the average sales, we can use the following query:

```sql
SELECT AVG(amount) FROM sales;
```

The result will be the average sales made by all employees.

## 2. SUM Function

The `SUM` function, on the other hand, calculates the total sum of a set of values in a numeric column. It returns the sum as a single value.

The syntax for using the `SUM` function is as follows:

```sql
SELECT SUM(column_name) FROM table_name;
```

Continuing with our example of the `sales` table, to calculate the total sales made by all employees, we can use the following query:

```sql
SELECT SUM(amount) FROM sales;
```

The result will be the sum of all sales made.

## Conclusion

In summary, the `AVG` function calculates the average of a set of values, while the `SUM` function calculates the total sum of a set of values. Use `AVG` when you want to find the average value, and use `SUM` when you want to find the total sum of values.

#hashtags: #SQL #aggregation