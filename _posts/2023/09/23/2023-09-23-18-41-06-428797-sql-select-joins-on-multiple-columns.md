---
layout: post
title: "SQL SELECT joins on multiple columns"
description: " "
date: 2023-09-23
tags: [Join]
comments: true
share: true
---

In SQL, joins are used to combine data from multiple tables based on a common column. While most examples showcase joins on a single column, there may be scenarios where you need to perform joins on multiple columns to achieve the desired results. This blog post will explain how to perform SQL joins on multiple columns.

## Inner Join on Multiple Columns

To perform an inner join on multiple columns, you can use the `ON` keyword followed by the join condition. Here's an example:

```sql
SELECT * 
FROM table1
INNER JOIN table2
ON table1.column1 = table2.column1
AND table1.column2 = table2.column2;
```

In this example, we are joining `table1` and `table2` using two columns `column1` and `column2`. The returned result will contain only the records where both column values match in both tables.

## Left Join on Multiple Columns

To perform a left join on multiple columns, you can use the same syntax as the inner join. Here's an example:

```sql
SELECT * 
FROM table1
LEFT JOIN table2
ON table1.column1 = table2.column1
AND table1.column2 = table2.column2;
```

This will return all records from `table1` and matching records from `table2` based on the values of `column1` and `column2`. If no matching records are found, `NULL` values will be returned for the columns of `table2`.

## Right Join on Multiple Columns

Similar to the left join, a right join on multiple columns can be achieved with the same syntax. Here's an example:

```sql
SELECT * 
FROM table1
RIGHT JOIN table2
ON table1.column1 = table2.column1
AND table1.column2 = table2.column2;
```

This will return all records from `table2` and matching records from `table1` based on the values of `column1` and `column2`. If no matching records are found, `NULL` values will be returned for the columns of `table1`.

## Conclusion

Performing joins on multiple columns in SQL allows you to combine data from different tables based on multiple criteria. Whether you need to perform an inner join, left join, or right join, the process is similar to joining on a single column. By specifying the join conditions using the `ON` keyword, you can achieve powerful data consolidation in your SQL queries.

#SQL #Join