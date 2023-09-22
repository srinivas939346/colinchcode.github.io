---
layout: post
title: "Non-clustered index and index seek vs index scan in SQL"
description: " "
date: 2023-09-22
tags: [Database, IndexOptimization]
comments: true
share: true
---

When it comes to optimizing the performance of a database, indexes play a crucial role. Indexes allow the database management system (DBMS) to quickly locate and retrieve the required data, improving query performance. In SQL, two commonly used index access methods are **index seek** and **index scan**. Let's explore the differences between them and when to use each.

## Non-clustered Index
A non-clustered index is a separate structure that stores a copy of selected columns from a table in a sorted order. This index structure points to the actual data rows. Non-clustered indexes are ideal for tables with frequent SELECT, UPDATE, or DELETE operations, as they reduce the I/O cost.

With non-clustered indexes, the DBMS can quickly locate the data typically by performing a two-step process. First, it searches the index tree to find the row or rows matching the search condition. Next, it retrieves the actual data by using the pointers in the index.

## Index Seek
Index seek is an operation that uses the non-clustered index to locate specific rows based on search criteria. When a query predicate matches the indexed columns, the DBMS can perform an index seek to directly access the required data pages. Index seeks are efficient and often result in lower resource usage since only the relevant rows need to be accessed.

Index seeks are best suited for queries with search criteria that match the indexed columns, particularly when the number of matching rows is relatively small. They are generally faster than index scans because they minimize disk I/O and read a smaller amount of data.

## Index Scan
Index scan is an operation that involves scanning the entire non-clustered index to retrieve the relevant data. Unlike index seek, which directly accesses only the necessary data pages, index scan reads all the index pages and then fetches the required rows from the corresponding data pages.

Index scans are more appropriate when there is a need to retrieve a large subset of rows or to retrieve all the rows from a table. They are typically slower than index seeks because they involve reading more data pages from disk.

## When to Use Each?

* Use **non-clustered indexes** when you want to improve the performance of SELECT, UPDATE, and DELETE operations on specific columns.
* Use **index seeks** when you have a small number of matching rows for a search condition and want to retrieve them efficiently.
* Use **index scans** when you need to access a large subset of rows or when you want to retrieve all the rows from a table.

It's important to note that the effectiveness of index seek or index scan depends on factors such as the size of the table, the selectivity of the search condition, and the overall database design. Monitoring query performance and considering the execution plan provided by the DBMS can help determine the most suitable index access method for a given scenario.

*#SQL #Database #IndexOptimization*