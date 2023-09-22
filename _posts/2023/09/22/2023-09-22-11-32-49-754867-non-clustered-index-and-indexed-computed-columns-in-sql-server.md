---
layout: post
title: "Non-clustered index and indexed computed columns in SQL Server"
description: " "
date: 2023-09-22
tags: [hashtags, SQLServer]
comments: true
share: true
---

In SQL Server, indexes play a crucial role in optimizing query performance. One type of index is the **non-clustered index**, which can greatly improve the efficiency of data retrieval operations.

## What is a Non-clustered Index?

A non-clustered index is an ordered data structure that contains a copy of selected columns from a table or view. It is stored separately from the table and is created based on one or more columns that are not part of the primary key. Unlike the clustered index, which determines the physical order of the data in a table, a non-clustered index does not alter the ordering of the data.

## Benefits of Non-clustered Index

- **Improved Query Performance**: Non-clustered indexes provide quicker access to data, as the queries can utilize the index to locate specific rows more efficiently.
- **Reduced Disk I/O**: By using non-clustered indexes, the number of disk I/O operations can be reduced, resulting in faster data retrieval.
- **Covering Queries**: Non-clustered indexes can include additional columns that are not in the index key, allowing queries to be satisfied entirely from the index without accessing the underlying table.

## Creating a Non-clustered Index

To create a non-clustered index, you can use the `CREATE INDEX` statement. Here's an example:

```sql
CREATE NONCLUSTERED INDEX idx_CustomerName
ON Customers (LastName, FirstName);
```

In this example, a non-clustered index named `idx_CustomerName` is created on the `Customers` table, using the `LastName` and `FirstName` columns.

## Indexed Computed Columns

In addition to indexing regular columns, SQL Server also allows you to create indexes on **computed columns**. Computed columns are virtual columns that derive their values using an expression or a combination of other columns in the table.

By indexing a computed column, you can improve query performance when filtering or ordering based on the computed value.

To create an index on a computed column, you can use the `CREATE INDEX` statement with the `PERSISTED` keyword. Here's an example:

```sql
ALTER TABLE Orders
ADD TotalAmount AS (Quantity * UnitPrice) PERSISTED;

CREATE NONCLUSTERED INDEX idx_TotalAmount
ON Orders (TotalAmount);
```

In this example, a computed column `TotalAmount` is added to the `Orders` table, representing the product of `Quantity` and `UnitPrice`. Then, a non-clustered index named `idx_TotalAmount` is created on the `TotalAmount` column.

#hashtags: #SQLServer #Indexing