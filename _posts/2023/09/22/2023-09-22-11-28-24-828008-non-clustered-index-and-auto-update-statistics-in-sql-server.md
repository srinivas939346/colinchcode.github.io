---
layout: post
title: "Non-clustered index and auto update statistics in SQL Server"
description: " "
date: 2023-09-22
tags: []
comments: true
share: true
---

When working with relational databases, optimizing query performance is crucial. One way to improve query performance is by using **indexes**. In SQL Server, there are two types of indexes - **clustered** and **non-clustered**.

A **non-clustered index** is a separate structure that contains a sorted copy of selected columns from a table. Unlike a clustered index, a non-clustered index does not determine the physical order of data in a table. Instead, it provides a faster way to look up data based on the indexed columns.

To create a non-clustered index in SQL Server, you can use the `CREATE INDEX` statement. Here is an example:

```sql
CREATE INDEX idx_name ON table_name (column1, column2);
```

In the above example, `idx_name` is the name of the index, `table_name` is the name of the table, and `column1` and `column2` are the columns on which the index is created.

When a query is executed that utilizes the non-clustered index, SQL Server can quickly locate the required data by looking up the index. This can significantly improve the performance of SELECT, JOIN, and WHERE clauses involving the indexed columns.

However, it is essential to note that while non-clustered indexes enhance read performance, they can slow down write operations like INSERT, UPDATE, and DELETE. Therefore, careful consideration and testing are necessary while deciding which columns to index.

# Auto Update Statistics in SQL Server

SQL Server uses statistics to estimate the selectivity of queries and generate efficient query execution plans. These statistics are automatically created and updated by SQL Server to provide up-to-date information for the query optimizer.

By default, SQL Server **automatically updates statistics** when a threshold number of changes in the underlying data occurs. This ensures that the query optimizer has access to accurate and relevant statistics for generating efficient execution plans.

To enable or disable the auto update statistics feature for a specific table or index, you can use the `ALTER TABLE` or `ALTER INDEX` statement with the `AUTO_UPDATE_STATISTICS` option. Here is an example:

```sql
-- To enable auto update statistics
ALTER TABLE table_name SET AUTO_UPDATE_STATISTICS ON;
-- OR
ALTER INDEX index_name ON table_name SET AUTO_UPDATE_STATISTICS ON;

-- To disable auto update statistics
ALTER TABLE table_name SET AUTO_UPDATE_STATISTICS OFF;
-- OR
ALTER INDEX index_name ON table_name SET AUTO_UPDATE_STATISTICS OFF;
```

It is generally recommended to keep the auto update statistics feature enabled as it ensures the query optimizer has the most accurate information for generating efficient execution plans. However, in some cases, disabling auto update statistics and manually updating the statistics when necessary might be preferred.