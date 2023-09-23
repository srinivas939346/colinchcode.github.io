---
layout: post
title: "SQL SELECT max with subqueries"
description: " "
date: 2023-09-23
tags: [subqueries]
comments: true
share: true
---

In SQL, the `SELECT MAX` statement is used to retrieve the highest value from a specific column in a table. Subqueries can be used in combination with `SELECT MAX` to further refine the result. Subqueries are enclosed in parentheses and can be used in various clauses such as `WHERE`, `FROM`, or `HAVING`.

Let's look at some examples to understand how to use `SELECT MAX` with subqueries effectively.

## Example 1: Retrieve the Maximum Value from a Column

Suppose we have a table named `employees` with columns `id`, `name`, and `salary`. We can use the following query to fetch the maximum salary from the table:

```sql
SELECT MAX(salary) AS max_salary
FROM employees;
```

Here, the `MAX` function is used to calculate the highest value in the `salary` column. The `AS` keyword is used to give the calculated value an alias for better readability.

## Example 2: Retrieve Records Based on the Maximum Value

To retrieve records that match the maximum value of a column, we can use a subquery with the `WHERE` clause. Let's say we want to retrieve employees who have the maximum salary:

```sql
SELECT id, name, salary
FROM employees
WHERE salary = (SELECT MAX(salary) FROM employees);
```

In this example, the subquery `(SELECT MAX(salary) FROM employees)` returns the highest salary from the `employees` table. The outer query uses this value in the `WHERE` clause to filter records that match the maximum salary.

## Example 3: Retrieve Maximum Value from a Subquery

Instead of specifying a column from a table, we can also use a subquery to calculate the maximum value. For instance, if we have another table called `departments` with columns `department_id` and `name`, and we want to find the department with the maximum number of employees, we can use the following query:

```sql
SELECT name
FROM departments
WHERE department_id = (
  SELECT department_id
  FROM employees
  GROUP BY department_id
  HAVING COUNT(*) = (
    SELECT MAX(emp_count)
    FROM (
      SELECT COUNT(*) AS emp_count
      FROM employees
      GROUP BY department_id
    ) AS subquery
  )
);
```

In this example, the innermost subquery `(SELECT COUNT(*) AS emp_count FROM employees GROUP BY department_id) AS subquery` calculates the number of employees in each department. The subquery `(SELECT MAX(emp_count) FROM subquery)` returns the maximum value of employee counts. Finally, the outermost query retrieves the department name that matches the maximum employee count.

## Conclusion

Using the `SELECT MAX` statement with subqueries provides a powerful way to extract data based on the highest value in a column. By combining these SQL techniques, you can perform complex queries and retrieve the desired results efficiently. Remember to use appropriate table and column names in your actual queries to reflect the structure of your own database.

#SQL #subqueries