---
layout: post
title: "SQL SELECT joins with null values"
description: " "
date: 2023-09-23
tags: [JOIN, NULL]
comments: true
share: true
---

When working with relational databases, it is common to use `JOIN` statements to combine data from multiple tables. However, when one of the tables has NULL values for the column you are joining on, it can cause unexpected results. In this blog post, we will explore how to handle such situations and ensure that your SQL queries return the desired results.

## Inner Join vs. Left Join

The two commonly used join types in SQL are `INNER JOIN` and `LEFT JOIN`. Let's take a look at how they handle NULL values in the join column:

### Inner Join

An `INNER JOIN` only returns rows where there is a match between the join columns in both tables. If one of the join columns has a NULL value, it will not be considered a match, and the row will be excluded from the result set.

```sql
SELECT table1.column1, table2.column2
FROM table1
INNER JOIN table2 ON table1.join_column = table2.join_column;
```

### Left Join

A `LEFT JOIN`, also known as a "left outer join," returns all rows from the left table (table1) and the matching rows from the right table (table2). If a row from the left table does not have a corresponding match in the right table, NULL values will be returned for the columns of the right table.

```sql
SELECT table1.column1, table2.column2
FROM table1
LEFT JOIN table2 ON table1.join_column = table2.join_column;
```

## Handling Null Values

To explicitly include NULL values in your join, you can add an additional condition in the `ON` clause using the `IS NULL` or `IS NOT NULL` operators. This way, you can get the desired result set that includes NULL values in the join column.

### Including NULL values

In this example, we want to include rows with NULL values in the join column from table1:

```sql
SELECT table1.column1, table2.column2
FROM table1
LEFT JOIN table2 ON table1.join_column = table2.join_column
   OR (table1.join_column IS NULL AND table2.join_column IS NULL);
```

### Excluding NULL values

Conversely, if you want to exclude rows with NULL values in the join column, you can add a condition to filter them out:

```sql
SELECT table1.column1, table2.column2
FROM table1
LEFT JOIN table2 ON table1.join_column = table2.join_column
WHERE table1.join_column IS NOT NULL AND table2.join_column IS NOT NULL;
```

## Conclusion

Understanding how different SQL joins handle NULL values is crucial for writing accurate queries. By using `INNER JOIN` or `LEFT JOIN` with appropriate conditions based on your requirements, you can manipulate the result set to include or exclude NULL values in the join column. This flexibility allows you to generate accurate and meaningful insights from your data.

#SQL #JOIN #NULL