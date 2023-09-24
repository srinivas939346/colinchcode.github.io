---
layout: post
title: "Combining SQL AVG with other functions like MAX and MIN"
description: " "
date: 2023-09-24
tags: [Database]
comments: true
share: true
---

In SQL, the **AVG** function is used to calculate the average value of a specific column in a table. However, there are scenarios where you might need to combine the AVG function with other aggregate functions like **MAX** and **MIN** to gain more insights from your data.

Let's explore some examples of how to combine these functions in SQL queries.

## Example 1: Finding the Average, Maximum, and Minimum of a Column

Suppose we have a table called `employees` with the following columns: `id`, `name`, and `salary`. To find the average, maximum, and minimum salary of all employees, we can use the following SQL query:

```sql
SELECT AVG(salary) AS average_salary,
       MAX(salary) AS maximum_salary,
       MIN(salary) AS minimum_salary
FROM employees;
```
By executing this query, we'll get a result set with three columns: `average_salary`, `maximum_salary`, and `minimum_salary`. These columns will contain the calculated average, maximum, and minimum salary values across all employees, respectively.

## Example 2: Combining AVG with Other Aggregate Functions on Grouped Data

Another common scenario is to calculate the average along with other aggregate functions on grouped data. Suppose we want to find the average salary, maximum salary, and minimum salary for each department in our `employees` table.

To accomplish this, we can use the following SQL query:

```sql
SELECT department,
       AVG(salary) AS average_salary,
       MAX(salary) AS maximum_salary,
       MIN(salary) AS minimum_salary
FROM employees
GROUP BY department;
```

By grouping the data by the `department` column and applying the AVG, MAX, and MIN functions, we can get the desired result set that shows the average, maximum, and minimum salary for each department.

## Conclusion

Combining the SQL `AVG` function with other aggregate functions like `MAX` and `MIN` can provide valuable insights into your data. Whether you need to find the overall average, maximum, and minimum values or perform calculations on grouped data, SQL offers a variety of functions to help you achieve those results.

Remember to use the appropriate **GROUP BY** clause when working with grouped data and include the necessary columns in your SELECT statement to display the desired calculations.

#SQL #Database