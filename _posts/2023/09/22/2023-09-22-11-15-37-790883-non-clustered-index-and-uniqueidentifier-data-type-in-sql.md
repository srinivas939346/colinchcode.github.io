---
layout: post
title: "Non-clustered index and uniqueidentifier data type in SQL"
description: " "
date: 2023-09-22
tags: [nonclusteredindex, uniqueidentifier]
comments: true
share: true
---

In SQL, a non-clustered index is a data structure that improves the performance of queries by allowing faster data retrieval. Unlike a clustered index where the physical order of the table is determined by the index, a non-clustered index is stored separately from the data rows.

When creating a non-clustered index, SQL Server creates a separate index structure that contains a copy of the indexed columns and a pointer to the physical location of the actual data rows. This allows for efficient searching and sorting based on the indexed columns.

To create a non-clustered index in SQL, you can use the `CREATE INDEX` statement followed by the `ON` clause specifying the table and the column(s) to be indexed. Here's an example:

```sql
CREATE NONCLUSTERED INDEX IX_Employee_LastName
ON Employees (LastName);
```

In the above example, we create a non-clustered index called `IX_Employee_LastName` on the `LastName` column of the `Employees` table.

# Uniqueidentifier Data Type in SQL

The `uniqueidentifier` data type in SQL is used to store globally unique identifiers (GUIDs). A GUID is a 128-bit value that is generated using an algorithm and is almost guaranteed to be unique across all devices and systems.

The `uniqueidentifier` data type is useful when you need to generate unique values for primary keys or when you need to store unique identifiers for various entities in your database.

To declare a column with the `uniqueidentifier` data type, you can use the following syntax:

```sql
CREATE TABLE MyTable
(
    ID uniqueidentifier PRIMARY KEY,
    Name varchar(50)
);
```

In the above example, we create a table called `MyTable` with a primary key column `ID` of type `uniqueidentifier`. The primary key constraint ensures that each value in the `ID` column is unique.

Using the `uniqueidentifier` data type can be helpful when you need to generate unique identifiers for records in your database, especially when the records are intended to be shared or synced across multiple systems or devices.

# #SQL #nonclusteredindex #uniqueidentifier