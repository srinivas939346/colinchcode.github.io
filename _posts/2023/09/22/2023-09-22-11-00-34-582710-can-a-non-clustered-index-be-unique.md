---
layout: post
title: "Can a non-clustered index be unique?"
description: " "
date: 2023-09-22
tags: [database, index]
comments: true
share: true
---

When creating a non-clustered index, you have the option to specify whether it should be unique or not. A unique non-clustered index ensures that the indexed values are unique across the indexed columns. This means that no two rows in the table can have the same values for the indexed columns.

To create a unique non-clustered index in SQL Server, you can use the following syntax:

```sql
CREATE UNIQUE NONCLUSTERED INDEX index_name
ON table_name (column1, column2, ...)
```

In the above code, `index_name` is the name you give to the index, `table_name` is the name of the table, and `column1`, `column2`, etc. are the columns you want to include in the index.

Using a unique non-clustered index can provide benefits like faster data retrieval and improved query performance, especially when querying data based on the indexed columns. However, it's important to note that creating too many unique indexes on a table can have a negative impact on the performance of data modification operations (e.g., inserts, updates, deletes).

So, to answer your question, yes, a non-clustered index can be unique, and it can be a useful tool for managing data integrity and improving query performance in database systems. #database #index