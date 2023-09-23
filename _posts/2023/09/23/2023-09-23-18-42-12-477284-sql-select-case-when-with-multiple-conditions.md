---
layout: post
title: "SQL SELECT case when with multiple conditions"
description: " "
date: 2023-09-23
tags: []
comments: true
share: true
---

Here's an example scenario: let's say you have a table called `employees` that contains information about employees in a company. You want to retrieve the employee names along with a custom label based on their salaries. 

```sql
SELECT 
  employee_name,
  CASE 
    WHEN salary > 50000 THEN 'High Earner'
    WHEN salary > 30000 THEN 'Moderate Earner'
    ELSE 'Low Earner'
  END AS salary_label
FROM employees;
```

In the above code snippet, we use the `CASE WHEN` statement with multiple conditions to determine the salary label. 

- If the `salary` is greater than 50,000, the employee will be labeled as a "High Earner". 
- If the `salary` is between 30,000 and 50,000, the employee will be labeled as a "Moderate Earner". 
- If the `salary` is less than or equal to 30,000, the employee will be labeled as a "Low Earner". 

The `CASE WHEN` statement evaluates each condition in sequence and returns the corresponding value for the first true condition. If none of the conditions are true, it executes the `ELSE` block. 

You can include as many conditions as needed by chaining `WHEN` statements. This allows for more flexibility in assigning values based on complex logic. 

Using `CASE WHEN` with multiple conditions provides a powerful way to transform and categorize data in your SQL queries. It allows you to apply different rules based on the specific conditions you define.