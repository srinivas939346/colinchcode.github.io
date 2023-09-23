---
layout: post
title: "SQL SELECT case when with joins"
description: " "
date: 2023-09-23
tags: [Joins]
comments: true
share: true
---

In SQL, the `CASE WHEN` statement is a powerful tool for conditional logic within a query. It allows you to specify different actions based on conditions, making it useful for complex data transformations. When combined with joins, it becomes even more versatile because you can perform conditional operations on multiple tables simultaneously.

Let's explore how to use `CASE WHEN` statements with SQL joins by considering a fictional scenario: a company that stores information about its employees and their departments in two separate tables.

## Employees Table

```sql
CREATE TABLE employees (
  employee_id INT PRIMARY KEY,
  employee_name VARCHAR(50),
  department_id INT
);
```

## Departments Table

```sql
CREATE TABLE departments (
  department_id INT PRIMARY KEY,
  department_name VARCHAR(50)
);
```

To retrieve data from both tables and apply a conditional operation, we can perform a SQL join using the `JOIN` keyword. Let's assume we want to retrieve employee names and their department names, but for employees without a department, we want to display "Not Assigned" instead.

Here's an example query that achieves this:

```sql
SELECT
  employees.employee_name,
  CASE WHEN departments.department_name IS NULL THEN 'Not Assigned' ELSE departments.department_name END AS department_name
FROM employees
LEFT JOIN departments ON employees.department_id = departments.department_id;
```

In this query:

- We select the `employee_name`, and use a `CASE WHEN` statement to determine the value for `department_name`.
- We check if `department_name` is `NULL` using the condition `departments.department_name IS NULL`. If it is `NULL`, we assign the value 'Not Assigned'. Otherwise, we use the actual department name.
- The `LEFT JOIN` ensures that all employees, regardless of whether they have a department or not, are included in the result set.

By using the `CASE WHEN` statement within the `SELECT` clause and combining it with joins, we can perform conditional operations on multiple tables to construct more meaningful data sets.

Remember to adjust the table and column names according to your own database structure. Don't forget to add proper indexes to optimize the performance of your queries!

#SQL #Joins