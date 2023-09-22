---
layout: post
title: "Non-clustered index and indexed views in SQL Server"
description: " "
date: 2023-09-22
tags: [SQLServer, Indexing]
comments: true
share: true
---

When it comes to optimizing query performance in SQL Server, non-clustered indexes play a crucial role. They provide a way to retrieve data quickly by organizing the data in a specific order and allowing efficient searching based on the indexed column(s).

## What are Non-Clustered Indexes?

A non-clustered index is a data structure that enhances the speed of data retrieval operations by creating a separate object in the database. Unlike a clustered index, a non-clustered index does not change the physical order of the table. Instead, it creates a separate structure that contains key values and pointers to the actual data rows.

## Benefits of Non-Clustered Indexes

1. **Faster Query Execution**: Non-clustered indexes allow the database engine to locate the required data more efficiently, resulting in faster query execution times.

2. **Reduced Data Storage**: Unlike clustered indexes, non-clustered indexes do not dictate the physical order of the data. This allows for a more compact storage footprint, saving disk space.

3. **Flexibility**: Non-clustered indexes can be created on one or more columns, providing flexibility in optimizing query performance for different scenarios.

## Creating Non-Clustered Indexes

To create a non-clustered index in SQL Server, you can use the `CREATE INDEX` statement followed by the table name, the indexed column(s), and the index name. Here's an example:

```sql
CREATE INDEX idx_name ON table_name (column1, column2);
```

Use the appropriate column(s) that are frequently used in search conditions or join operations to maximize the benefits of the non-clustered index.

## Indexed Views: A Performance Boosting Technique

Indexed views are another powerful technique for improving query performance in SQL Server. An indexed view is a precomputed result set that is stored and indexed in the database. This allows the database engine to directly access the summarized data, eliminating the need for joins and aggregations during query execution.

## Benefits of Indexed Views

1. **Improved Query Performance**: Indexed views can significantly improve query performance by providing a precomputed, optimized result set. This is especially useful for complex queries involving aggregations or joins.

2. **Reduced Storage and CPU Overhead**: By storing the precomputed view, the database engine can minimize the need for expensive computations during query execution, resulting in reduced CPU usage and improved overall system performance.

## Creating Indexed Views

Creating an indexed view involves two steps:
1. Create the view: Use the `CREATE VIEW` statement to define the view.
2. Create the index: Use the `CREATE UNIQUE CLUSTERED INDEX` or `CREATE UNIQUE NONCLUSTERED INDEX` statement to create an index on the view.

Here's an example:

```sql
-- Step 1: Create the view
CREATE VIEW vw_name
AS
SELECT column1, column2, AVG(column3) AS average
FROM table_name
GROUP BY column1, column2;

-- Step 2: Create the index on the view
CREATE UNIQUE CLUSTERED INDEX idx_name ON vw_name (column1, column2);
```

Remember to adjust the view definition and index based on your specific requirements.

#SQLServer #Indexing