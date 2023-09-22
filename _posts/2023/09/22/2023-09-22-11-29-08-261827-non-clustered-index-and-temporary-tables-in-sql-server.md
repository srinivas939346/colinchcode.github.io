---
layout: post
title: "Non-clustered index and temporary tables in SQL Server"
description: " "
date: 2023-09-22
tags: [temp_orders, temp_orders]
comments: true
share: true
---

In SQL Server, an index is a powerful feature used to improve the performance of database queries. While a clustered index determines the physical order of data in a table, a non-clustered index provides an alternate logical order. It organizes data in separate structure apart from the actual table, allowing for faster retrieval of data based on the indexed columns.

## How does a non-clustered index work?

A non-clustered index consists of a separate structure that stores a copy of the indexed columns and a pointer to the corresponding rows in the table. This structure is ordered based on the indexed columns, enabling efficient searching and retrieval of data. When a query references the indexed columns, SQL Server uses the non-clustered index to locate the data quickly by traversing the index structure.

## Benefits of using a non-clustered index

1. Improved query performance: Non-clustered indexes enable faster retrieval of data by reducing the number of disk I/O operations required. They can significantly speed up data access for columns frequently used in search conditions, joins, and sorting operations.

2. Minimal impact on data modification operations: Since non-clustered indexes are stored separately from the table, they can be updated more efficiently than clustered indexes. This leads to minimal performance overhead when performing data modifications such as inserts, updates, and deletes.

## Creating a non-clustered index in SQL Server

To create a non-clustered index on a table in SQL Server, you can use the `CREATE INDEX` statement. Here's an example:

```sql
CREATE NONCLUSTERED INDEX idx_employee_lastname ON Employees (LastName);
```

In this example, we're creating a non-clustered index named `idx_employee_lastname` on the `LastName` column of the `Employees` table.

# Temporary Tables in SQL Server

Temporary tables are a unique feature in SQL Server that allow you to store and process intermediate results within a session. They are particularly useful when you need to store temporary data that is specific to a particular operation or session.

## How are temporary tables different from regular tables?

Unlike regular tables, temporary tables are created in `tempdb`, a system database in SQL Server dedicated to temporary objects. They exist only for the duration of a session or transaction and are automatically dropped when the session ends or the transaction is rolled back.

## Benefits of using temporary tables

1. Data isolation: Temporary tables provide a private workspace within a session, ensuring data isolation from other concurrent sessions. This is especially useful when multiple users are working on similar operations simultaneously.

2. Query optimization: Temporary tables allow you to break down complex queries into simpler steps. By storing intermediate results in temporary tables, you can optimize performance by reducing the complexity of the overall query.

## Creating and using temporary tables in SQL Server

To create a temporary table in SQL Server, you can use the `CREATE TABLE` statement with the `#` prefix for local temporary tables, or `##` prefix for global temporary tables. Here's an example:

```sql
CREATE TABLE #temp_orders
(
   OrderID INT,
   OrderDate DATETIME,
   CustomerID INT
);
```

In this example, we're creating a local temporary table named `#temp_orders` with three columns: `OrderID`, `OrderDate`, and `CustomerID`.

To insert data into a temporary table and use it in queries, you can follow the same syntax as regular tables:

```sql
INSERT INTO #temp_orders (OrderID, OrderDate, CustomerID)
VALUES (1, '2022-01-01', 123), (2, '2022-01-02', 456);

SELECT * FROM #temp_orders;
```

In this example, we're inserting two rows into the temporary table and then selecting all rows from it.

#hashtags #SQLServer #indexing