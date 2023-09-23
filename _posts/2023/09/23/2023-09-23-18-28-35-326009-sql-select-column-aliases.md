---
layout: post
title: "SQL SELECT column aliases"
description: " "
date: 2023-09-23
tags: [ColumnAliases]
comments: true
share: true
---

In SQL, column aliases allow you to assign temporary names or labels to the columns returned by a SELECT query. These aliases can make your query results more readable and can be useful when dealing with complex queries or when joining multiple tables. In this blog post, we will explore how to use column aliases in SELECT statements.

## Basic Syntax

The basic syntax for using column aliases in a SELECT statement is as follows:

```sql
SELECT column_name AS alias_name
FROM table_name;
```

Here, `column_name` refers to the actual name of the column in the table, and `alias_name` refers to the temporary name you want to assign to that column.

## Example

Let's consider a simple example where we have a table named `employees` with columns `first_name`, `last_name`, and `salary`. We want to list all the employees with their salaries, but we want to display the salary column with the alias name `Salary`.

```sql
SELECT first_name, last_name, salary AS Salary
FROM employees;
```

In the above example, we used the `AS` keyword to assign the alias name `Salary` to the `salary` column. The result of the query will include columns `first_name`, `last_name`, and `Salary`, where `Salary` represents the value of the `salary` column.

## Calculated Columns

Column aliases can also be used to create calculated columns in a SELECT statement. This can be helpful when you need to perform calculations on existing columns and present the results with a different label. 

For example, suppose we have a table named `orders` with columns `order_id`, `order_date`, and `total_amount`. We want to calculate the average order amount per day and display it as `avg_order_amount`.

```sql
SELECT AVG(total_amount) AS avg_order_amount
FROM orders
GROUP BY order_date;
```

In the above example, we used the `AVG()` function to calculate the average `total_amount` for each `order_date`. We assigned the alias name `avg_order_amount` to the calculated column. The result of the query will include the `avg_order_amount` column representing the average order amount per day.

## Conclusion

Column aliases are a powerful feature in SQL that allow you to assign temporary names to columns in your query results. You can use them to make your results more readable, create calculated columns, or perform other transformations on the data. By understanding and utilizing column aliases, you can enhance the clarity and efficiency of your SQL queries.

### #SQL #ColumnAliases