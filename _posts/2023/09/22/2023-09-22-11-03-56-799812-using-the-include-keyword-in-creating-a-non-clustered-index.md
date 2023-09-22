---
layout: post
title: "Using the INCLUDE keyword in creating a non-clustered index"
description: " "
date: 2023-09-22
tags: [database, nonclusteredindex]
comments: true
share: true
---

When it comes to optimizing the performance of your database queries, creating indexes plays a crucial role. Indexes help in improving query execution time and overall system performance. When creating non-clustered indexes, the **INCLUDE** keyword can be used to further enhance the effectiveness of these indexes.

## What is a Non-Clustered Index?

Before diving into the **INCLUDE** keyword, it's important to understand what a non-clustered index is. A non-clustered index is a type of index in a database that stores a copy of the indexed columns, along with a pointer to the actual data rows. This index structure allows for efficient data retrieval based on the indexed columns.

## The Importance of the INCLUDE Keyword

By default, when you create a non-clustered index, only the indexed columns are stored in the index structure. However, there may be scenarios where including additional columns in the index can significantly improve query performance.

Consider a scenario where you have a table with multiple columns, and you frequently run queries that require retrieving specific columns from this table. If you include these frequently accessed columns in the non-clustered index using the **INCLUDE** keyword, it eliminates the need for the database engine to perform an additional lookup in the original table. This, in turn, leads to improved query performance.

## Example Usage of the INCLUDE Keyword

Let's take a look at an example to understand how to use the **INCLUDE** keyword in creating a non-clustered index. Suppose we have a table called `Employees` with the following columns: `EmployeeID`, `FirstName`, `LastName`, `Email`, `DepartmentID`.

To create a non-clustered index that includes the `FirstName` and `LastName` columns, we can use the following SQL query:

```sql
CREATE NONCLUSTERED INDEX IX_Employees_Names
ON Employees (FirstName, LastName)
INCLUDE (Email)
```

In this example, we have created a non-clustered index called `IX_Employees_Names` on the `FirstName` and `LastName` columns. Additionally, we have included the `Email` column in the index using the **INCLUDE** keyword. This means that the index will contain the data from the indexed columns (`FirstName`, `LastName`) as well as the `Email` column.

## Benefits of Using the INCLUDE Keyword

The **INCLUDE** keyword offers several benefits when creating non-clustered indexes:

1. Improved Query Performance: By including frequently accessed columns in the index, queries can be executed more efficiently without the need for additional lookups.

2. Reduced Disk I/O: Including columns in the index can minimize disk I/O as data retrieval can be performed directly from the index structure instead of fetching data from the original table.

3. Smaller Index Size: By selectively including only necessary columns, the index size can be reduced, leading to optimized storage and memory usage.

## Conclusion

The **INCLUDE** keyword in non-clustered index creation is a powerful tool for enhancing query performance and optimizing database systems. By including frequently accessed columns, you can eliminate the need for additional lookups and improve overall query execution time. Consider utilizing the **INCLUDE** keyword strategically for better performance and efficiency in your database environment.

#database #nonclusteredindex