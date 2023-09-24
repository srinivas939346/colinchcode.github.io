---
layout: post
title: "Comparison of SQL AVG and AVGIFS functions in other databases"
description: " "
date: 2023-09-24
tags: []
comments: true
share: true
---

When working with databases, it is common to calculate the average of a set of values. In SQL, there are different ways to accomplish this task depending on the specific database you are using. In this article, we will compare the `AVG` function and the `AVGIFS` function in different databases.

## SQL `AVG` Function

The `AVG` function in SQL is a built-in aggregate function that calculates the average of a column or expression. It takes all values within a specified column and returns the average value.

The general syntax of the `AVG` function is as follows:
```sql
SELECT AVG(column_name)
FROM table_name;
```

Let's consider an example where we have a table named `employees` with a column `salary`:
```sql
SELECT AVG(salary)
FROM employees;
```
This query will return the average salary of all employees in the `employees` table.

### Pros of `AVG` Function
- **Simple Syntax**: The `AVG` function has a straightforward syntax, making it easy to use.
- **Wide Support**: It is widely supported across different databases, including MySQL, PostgreSQL, Oracle, and SQL Server.

### Cons of `AVG` Function
- **No Conditional Filtering**: The `AVG` function calculates the average of all values within the specified column, without the ability to filter based on conditions.

## SQL `AVGIFS` Function

Some databases provide additional functions like `AVGIFS` to address the limitations of the `AVG` function. These functions allow for average calculations with conditional filtering.

Let's compare how similar functionality is achieved in different databases:

### MySQL

In MySQL, the `AVG` function can be combined with a `WHERE` clause to achieve conditional filtering. For example:
```sql
SELECT AVG(salary)
FROM employees
WHERE department = 'Marketing';
```

### PostgreSQL

PostgreSQL provides the `AVG` function along with the `FILTER` clause, which allows for filtering based on conditions. For example:
```sql
SELECT AVG(salary)
FROM employees
WHERE department = 'Marketing'
GROUP BY department;
```

### Oracle

Oracle's `AVG` function can be used with a `CASE` statement to achieve conditional filtering. For example:
```sql
SELECT AVG(CASE WHEN department = 'Marketing' THEN salary END)
FROM employees;
```

### SQL Server

In SQL Server, the `AVG` function can be combined with the `WHERE` clause to filter based on conditions. For example:
```sql
SELECT AVG(salary)
FROM employees
WHERE department = 'Marketing';
```

### Pros of `AVGIFS` Functions
- **Conditional Filtering**: `AVGIFS` functions allow for calculating the average based on specified conditions.

### Cons of `AVGIFS` Functions
- **Database-Specific**: The availability and syntax of `AVGIFS` functions may vary across different database systems.

## Conclusion

In summary, the `AVG` function is a common SQL aggregate function that calculates the average of a column's values. However, some databases offer additional functions like `AVGIFS` to enable conditional filtering while computing the average. The choice between `AVG` and `AVGIFS` depends on the specific database you are using and its supported functions.