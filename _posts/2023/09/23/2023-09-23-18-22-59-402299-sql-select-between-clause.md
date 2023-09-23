---
layout: post
title: "SQL SELECT between clause"
description: " "
date: 2023-09-23
tags: [between]
comments: true
share: true
---

The syntax for using the `BETWEEN` clause in a `SELECT` statement is as follows:

```sql
SELECT column_name(s)
FROM table_name
WHERE column_name BETWEEN value1 AND value2;
```

Here's a breakdown of each part of the syntax:

- `column_name(s)`: Specify the name of the column(s) you want to retrieve or select.
- `table_name`: Specify the name of the table from which you want to retrieve the data.
- `column_name`: Specify the column on which you want to apply the `BETWEEN` condition.
- `value1` and `value2`: Specify the range of values within which you want to select records (inclusive).

To illustrate this with an example, let's say we have a table called `employees` with columns `id`, `name`, and `salary`. If we want to select employees with salaries between $50,000 and $100,000, the SQL query would look like this:

```sql
SELECT id, name, salary
FROM employees
WHERE salary BETWEEN 50000 AND 100000;
```

This query will retrieve the `id`, `name`, and `salary` of employees whose salary falls within the specified range.

Using the `BETWEEN` clause can be quite useful when you want to narrow down your search by specifying a range of values. However, keep in mind that the `BETWEEN` clause includes both the lower and upper bounds, so you need to be careful to choose the appropriate values for your condition.

#sql #between