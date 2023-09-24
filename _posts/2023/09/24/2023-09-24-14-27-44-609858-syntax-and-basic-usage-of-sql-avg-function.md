---
layout: post
title: "Syntax and basic usage of SQL AVG function"
description: " "
date: 2023-09-24
tags: []
comments: true
share: true
---

The basic syntax of the AVG function is as follows:

```
SELECT AVG(column_name)
FROM table_name
WHERE condition;
```

Here, the `AVG` keyword is followed by the name of the column from which you want to calculate the average. The `FROM` keyword is used to specify the table name from which the data is being retrieved. You can also add a `WHERE` clause to specify any additional conditions for calculating the average.

For example, let's say we have a table named `sales` with the following structure:

```
CREATE TABLE sales (
  id INT PRIMARY KEY,
  product_name VARCHAR(100),
  price DECIMAL(10, 2)
);
```

To calculate the average price of all products in the table, you can use the following SQL query:

```sql
SELECT AVG(price)
FROM sales;
```

If you want to calculate the average price of only the products with a specific condition, such as products with a price greater than $50, you can modify the query like this:

```sql
SELECT AVG(price)
FROM sales
WHERE price > 50;
```

It's important to note that the AVG function is typically used for numeric columns. If you try to use it on non-numeric columns, you may encounter an error.

Overall, the SQL AVG function is a useful tool for calculating the average value of numeric data in a database table. It can be used to perform various calculations and analysis on a dataset, providing valuable insights for decision-making. #SQL #AVG