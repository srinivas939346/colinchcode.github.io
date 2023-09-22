---
layout: post
title: "Non-clustered index and index visibility in SQL Server"
description: " "
date: 2023-09-22
tags: [SQLServer, NonClusteredIndex]
comments: true
share: true
---

In SQL Server, an index is a vital feature to enhance query performance. One type of index is the non-clustered index, which allows faster data retrieval by storing a copy of the indexed columns separately from the actual data.

## How Non-clustered Index Works

A non-clustered index creates a separate structure that includes the indexed columns and a pointer to the actual data rows. This index is stored outside of the table, allowing for quick lookup and retrieval of specific data based on the indexed columns.

When a query is executed that includes the indexed columns, SQL Server can directly access the non-clustered index to find the desired data rows, instead of scanning the entire table. This process significantly improves query performance, especially for large tables with frequent data retrievals.

## Non-clustered Index Visibility

One important aspect to consider is the visibility of non-clustered indexes. By default, non-clustered indexes are not visible to user queries. However, SQL Server provides the option to make the index visible, allowing the database engine to consider it during query optimization.

To make a non-clustered index visible, you can use the `INCLUDE` keyword during index creation or alteration. By including additional columns in the index, you provide more data values to the index structure, which can be beneficial for covering queries.

## Example Code

Here's an example of creating a visible non-clustered index in SQL Server:

```sql
CREATE NONCLUSTERED INDEX ix_example
ON dbo.TableName (IndexedColumn)
INCLUDE (AdditionalColumn1, AdditionalColumn2);
```

In the above code snippet, we create a non-clustered index named "ix_example" on the "TableName" table. The "IndexedColumn" is the primary indexed column, and "AdditionalColumn1" and "AdditionalColumn2" are included to cover more queries.

## Conclusion

Non-clustered indexes play a crucial role in improving query performance in SQL Server. By utilizing non-clustered indexes and making them visible, you can enhance the database's ability to efficiently retrieve data, resulting in faster query execution times.

#SQLServer #NonClusteredIndex