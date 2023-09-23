---
layout: post
title: "SQL SELECT distinct with nested selects"
description: " "
date: 2023-09-23
tags: [NestedSELECTs]
comments: true
share: true
---

In SQL, the `SELECT DISTINCT` statement is used to fetch unique rows from a table or a result set. It eliminates duplicate values and only returns distinct rows. 

Sometimes, you may need to use nested SELECTs with the `SELECT DISTINCT` statement to further refine your query. This allows you to perform more advanced filtering or calculations before obtaining the distinct records.

Let's look at an example to better understand how to use nested SELECTs with `SELECT DISTINCT`:

```sql
SELECT DISTINCT column_name
FROM (SELECT column_name
      FROM table_name
      WHERE condition
      ORDER BY column_name) AS subquery;
```

In this example, we have a subquery enclosed within parentheses. This subquery can contain any valid SQL statement, such as additional filtering conditions, sorting, or even joining multiple tables.

Let's break down the example:

1. Start with the inner SELECT statement in the subquery. This statement defines the columns to be selected and the table from which the data is fetched.
2. Apply any necessary conditions using the `WHERE` clause to filter the rows.
3. Use the `ORDER BY` clause if you want to sort the results in a specific order.
4. Enclose the subquery in parentheses and assign it an alias, such as `AS subquery`.
5. Use the outer `SELECT DISTINCT` statement to select the distinct values from the column(s) specified in the subquery.

By using nested SELECTs with `SELECT DISTINCT`, you can leverage the power of SQL to write more complex queries and obtain distinct records based on specific criteria.

Remember to replace `column_name` and `table_name` with the actual column and table names in your database. Adjust the conditions and sorting as per your requirements.

#SQL #NestedSELECTs