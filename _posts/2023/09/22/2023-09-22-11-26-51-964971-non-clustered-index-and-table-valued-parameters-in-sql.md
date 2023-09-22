---
layout: post
title: "Non-clustered index and table-valued parameters in SQL"
description: " "
date: 2023-09-22
tags: []
comments: true
share: true
---

When it comes to indexing in SQL Server, **non-clustered indexes** play a crucial role in improving query performance. Unlike **clustered indexes**, which determine the physical order of the data on disk, non-clustered indexes create a separate structure that provides quick access to the data.

The non-clustered index consists of a key column or columns that are stored separately from the data rows. This allows for efficient retrieval of data and improved query performance. Non-clustered indexes are useful when searching for specific values or performing JOIN operations.

To create a non-clustered index in SQL Server, you can use the `CREATE INDEX` statement. Here's an example:

```sql
CREATE NONCLUSTERED INDEX IX_Employee_LastName
ON Employees (LastName);
```

In the above example, we're creating a non-clustered index named `IX_Employee_LastName` on the `LastName` column of the `Employees` table.

It's important to note that while non-clustered indexes can improve query performance, they also come with some overhead during updates or inserts, as the index needs to be maintained. Therefore, it's essential to strike a balance between creating too many non-clustered indexes (which can slow down data modification operations) and having the right indexes to optimize query performance.

# Table-Valued Parameters in SQL Server

Table-valued parameters (TVPs) are a useful feature in SQL Server that allow you to pass a table structure as a parameter to a stored procedure or a function. This eliminates the need to pass data as comma-separated values or XML, simplifying data manipulation operations.

TVPs are beneficial when you need to pass multiple rows of data as a single parameter. For example, you can use TVPs to insert multiple records into a table, perform bulk updates, or join with other tables for complex queries.

To use table-valued parameters, you need to follow these steps:

1. Create a user-defined table type that defines the structure of the parameter.
2. Declare the table-valued parameter in your stored procedure or function.
3. Pass a table variable of the defined type as the parameter value.

Here's an example of creating and using a table-valued parameter:

```sql
-- Step 1: Create user-defined table type
CREATE TYPE EmployeeType AS TABLE (
    EmployeeID INT,
    FirstName VARCHAR(50),
    LastName VARCHAR(50)
);

-- Step 2: Declare table-valued parameter in stored procedure
CREATE PROCEDURE InsertEmployees
    @Employees EmployeeType READONLY
AS
BEGIN
    -- Step 3: Use table-valued parameter in stored procedure
    INSERT INTO Employees (EmployeeID, FirstName, LastName)
    SELECT EmployeeID, FirstName, LastName
    FROM @Employees;
END;
```

In the above example, we create a user-defined table type named `EmployeeType`, which represents the structure of the table-valued parameter. Then, we declare a stored procedure named `InsertEmployees`, which takes the `@Employees` parameter of type `EmployeeType READONLY`. Finally, we use the table-valued parameter to insert data into the `Employees` table.

By utilizing non-clustered indexes and table-valued parameters in SQL Server, you can significantly enhance query performance and simplify data manipulation operations, respectively. Consider using these features in your SQL Server projects to optimize your database performance and improve developer productivity.