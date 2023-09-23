---
layout: post
title: "SQL SELECT case statement"
description: " "
date: 2023-09-23
tags: [SELECT, CASE]
comments: true
share: true
---

In SQL, the CASE statement is a powerful tool that allows you to perform conditional logic in your SELECT queries. It enables you to control the flow of your query and return different values based on specific conditions.

## Syntax of the SQL SELECT CASE Statement

The general syntax of the SQL SELECT CASE statement is as follows:

```sql
SELECT 
  CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    ...
    ELSE result
  END AS column_alias
FROM table_name;
```

### Explanation of the Syntax

- The `CASE` keyword is followed by one or more `WHEN` clauses.
- Each `WHEN` clause specifies a condition that is checked for each row in the table.
- If a condition is true, the corresponding `THEN` result is returned.
- You can have multiple `WHEN` clauses to check for different conditions.
- The `ELSE` keyword is optional. If none of the conditions are true, the `ELSE` result is returned.
- The `END` keyword marks the end of the `CASE` statement.
- The `AS` keyword is used to assign a column alias to the result of the `CASE` statement.

## Example Usage

Let's consider a simple example where we have a `products` table with columns `product_id`, `product_name`, and `quantity`. We want to categorize the products based on their quantity as 'Low', 'Medium', or 'High'. Here's how we can achieve it using the SQL SELECT CASE statement:

```sql
SELECT 
  product_id, 
  product_name, 
  quantity,
  CASE
    WHEN quantity <= 10 THEN 'Low'
    WHEN quantity <= 50 THEN 'Medium'
    ELSE 'High'
  END AS quantity_category
FROM products;
```

In this example, we use the CASE statement to check the value of the `quantity` column for each row. Depending on the value, we assign the corresponding category ('Low', 'Medium', or 'High') to the `quantity_category` column.

By using the SQL SELECT CASE statement, you can perform complex logic and make your query results more meaningful and informative.

#SQL #SELECT #CASE