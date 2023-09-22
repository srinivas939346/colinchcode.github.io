---
layout: post
title: "Non-clustered index and filtered statistics in SQL Server"
description: " "
date: 2023-09-22
tags: [SQLServer, DatabaseOptimization]
comments: true
share: true
---

In the world of relational databases, optimizing query performance is crucial for ensuring efficient data retrieval. SQL Server offers several techniques to fine-tune query execution, and two of the commonly used features are non-clustered indexing and filtered statistics.

## Non-Clustered Indexing

**Non-clustered indexes** are separate data structures that provide an alternative physical ordering of the data in a table. This allows for faster retrieval of specific rows based on the indexed columns. Unlike clustered indexes that dictate the physical order of data, non-clustered indexes can be created on any column(s) of a table.

Creating a non-clustered index involves sorting the indexed column(s) values and maintaining a separate structure that points to the corresponding rows in the table. This helps SQL Server to quickly locate the required data during query execution, resulting in improved performance.

Example of creating a non-clustered index in SQL Server:

```sql
-- Create a non-clustered index on the 'LastName' column of 'Customers' table
CREATE NONCLUSTERED INDEX IX_Customers_LastName
ON Customers (LastName);
```

It's important to note that non-clustered indexes have a trade-off in terms of increased storage requirements and potentially slower insert, update, and delete operations. Therefore, careful consideration must be given when deciding which columns to index and where non-clustered indexes are most beneficial.

## Filtered Statistics

**Filtered statistics** provide a way to generate optimized execution plans for queries that access only a subset of rows in a table, based on a filter predicate. By creating filtered statistics, SQL Server can generate more accurate cardinality estimates for queries, leading to better query plans and ultimately, improved performance.

Filtered statistics are typically used when a significant portion of data in a table is accessed through specific filters or predicates. By gathering statistics only on the filtered subset of data, SQL Server can make better-informed decisions during query optimization.

Example of creating filtered statistics in SQL Server:

```sql
-- Create filtered statistics on 'Orders' table for orders placed in the year 2022
CREATE STATISTICS FK_Orders_OrderDate_2022
ON Orders (OrderDate)
WHERE OrderDate >= '2022-01-01' AND OrderDate < '2023-01-01';
```

Filtered statistics can be particularly useful in scenarios such as partitioned tables, data archiving, or handling large historical datasets where accessing a specific subset of data is a common requirement.

#SQLServer #DatabaseOptimization