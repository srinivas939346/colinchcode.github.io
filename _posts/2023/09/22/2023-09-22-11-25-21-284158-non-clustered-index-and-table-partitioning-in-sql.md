---
layout: post
title: "Non-clustered index and table partitioning in SQL"
description: " "
date: 2023-09-22
tags: [SQLIndexing, NonClusteredIndex]
comments: true
share: true
---

A Non-clustered index is a data structure that improves the performance of querying data in a SQL database. Unlike a clustered index, which determines the physical order of rows in a table, a non-clustered index creates a separate structure that contains the indexed columns and their corresponding row pointers.

**Why Use a Non-clustered Index?**
A non-clustered index is useful when you frequently query data based on columns other than the primary key or clustering key. It speeds up the retrieval of data by allowing the database engine to quickly locate the rows that meet the search criteria. This is particularly beneficial for large tables with millions of rows.

**Creating a Non-clustered Index**
To create a non-clustered index on a table, you can use the `CREATE INDEX` statement in SQL. Here's an example:

```sql
CREATE INDEX idx_name ON table_name (column1, column2, ...);
```

In this example, `idx_name` is the name of the index, `table_name` is the name of the table, and `column1, column2, ...` are the columns on which the index is created. You can add as many columns as necessary.

**Query Optimization with Non-clustered Index**
When executing a query that involves searching or filtering data based on the indexed columns, the database engine can utilize the non-clustered index to quickly locate the relevant rows. This reduces the need for scanning the entire table and improves the query performance.

However, it's important to note that non-clustered indexes come with a slight overhead when modifying data (inserting, updating, or deleting rows) in the indexed table. Each modification operation may require updating the index as well, which can slow down the overall performance.

**#SQLIndexing #NonClusteredIndex**


# Table Partitioning in SQL

Table partitioning is a technique used in SQL databases to divide a large table into smaller, more manageable partitions based on certain criteria. Each partition is stored as a separate physical unit with its own set of data, but they are logically treated as a single table. This approach offers several benefits, including improved query performance and easier data management.

**Why Use Table Partitioning?**
Partitioning a table provides several advantages, such as:
- **Improved Performance**: By dividing a large table into smaller partitions, query execution times can be significantly reduced, as the database engine only needs to scan the relevant partitions instead of the entire table.
- **Easier Data Management**: Partitioning allows for easier data archival, purging, and maintenance operations. You can easily remove or move entire partitions, which simplifies database management tasks.
- **Parallel Processing**: Some database systems can process multiple partitions in parallel, further enhancing performance in scenarios with multiple cores or distributed environments.

**Types of Table Partitioning**
There are various methods of partitioning a table, including:
- **Range Partitioning**: Partitioning based on a specified range or numeric value.
- **Hash Partitioning**: Partitioning based on a hash value calculated from one or more columns.
- **List Partitioning**: Partitioning based on predefined lists of values.
- **Composite Partitioning**: Combining multiple partitioning methods.

**Creating a Partitioned Table**
To create a partitioned table, you need to define a partition function that specifies the partitioning criterion and a partition scheme that determines where the data for each partition is stored. Here's a simplified example using range partitioning:

```sql
CREATE PARTITION FUNCTION pf_name (data_type)
AS RANGE LEFT FOR VALUES (value1, value2, ...);

CREATE PARTITION SCHEME ps_name
AS PARTITION pf_name
TO (filegroup1, filegroup2, ...);

CREATE TABLE partitioned_table
(
    column1 data_type,
    column2 data_type
)
ON ps_name (column1);
```

In this example, `pf_name` is the name of the partition function, `value1, value2, ...` are the values that define the partition boundaries, `ps_name` is the name of the partition scheme, and `filegroup1, filegroup2, ...` are the filegroups where the partitions are stored.

**#SQLPartitioning #TablePartition**