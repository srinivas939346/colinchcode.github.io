---
layout: post
title: "SQL SELECT logical operators"
description: " "
date: 2023-09-23
tags: [SELECT]
comments: true
share: true
---

Logical operators are used to combine multiple conditions in SQL SELECT statements. They allow you to filter and retrieve data based on multiple criteria. In this blog post, we will explore the commonly used logical operators in SQL SELECT statements.

### AND Operator

The `AND` operator is used to combine two or more conditions in a SQL SELECT statement. It retrieves rows that satisfy **all** of the specified conditions. Here's an example:

```sql
SELECT * FROM employees
WHERE age > 30 AND salary > 50000;
```

This query selects all rows from the `employees` table where the age is greater than 30 **and** the salary is greater than 50000.

### OR Operator

The `OR` operator is used to combine two or more conditions in a SQL SELECT statement. It retrieves rows that satisfy **any** of the specified conditions. Here's an example:

```sql
SELECT * FROM employees
WHERE department = 'HR' OR department = 'Finance';
```

This query selects all rows from the `employees` table where the department is either 'HR' **or** 'Finance'.

### NOT Operator

The `NOT` operator is used to negate a condition in a SQL SELECT statement. It retrieves rows that **do not** satisfy the specified condition. Here's an example:

```sql
SELECT * FROM employees
WHERE NOT department = 'IT';
```

This query selects all rows from the `employees` table where the department is not 'IT'.

### Combining Operators

You can combine logical operators to create more complex conditions in SQL SELECT statements. For example:

```sql
SELECT * FROM products
WHERE (price > 100 AND stock > 0) OR (category = 'Electronics' AND discount > 0.1);
```

This query selects all rows from the `products` table where the price is greater than 100 **and** the stock is greater than 0, **or** the category is 'Electronics' **and** the discount is greater than 0.1.

By understanding and utilizing these logical operators effectively, you can construct powerful SQL SELECT statements to retrieve precisely the data you need.

#SQL #SELECT