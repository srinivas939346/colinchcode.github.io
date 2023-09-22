---
layout: post
title: "What is the difference between a non-clustered index and a filtered index?"
description: " "
date: 2023-09-22
tags: [Database, Indexes]
comments: true
share: true
---

In database management systems, indexes play a crucial role in optimizing query performance. Among the various types of indexes, non-clustered indexes and filtered indexes are commonly used. While they both improve query performance, there are key differences between the two.

## Non-Clustered Index

A **non-clustered index** is a data structure that sorts and stores a copy of the indexed columns separately from the actual data. This allows for quicker data retrieval and sorting operations. When a non-clustered index is created, a separate index tree is constructed, and the leaf nodes of this tree contain the index keys and pointers to the actual data rows.

Here are a few key points about non-clustered indexes:
- They can be created on one or more columns of a table.
- They do not define the physical order of the data in the table.
- They provide a faster way to retrieve data than scanning the entire table.
- They consume additional disk space.

## Filtered Index

On the other hand, a **filtered index** is a special type of non-clustered index that includes only a subset of rows from a table. It is created with a filter predicate, allowing you to define specific conditions that the indexed rows must satisfy. A filtered index can be a useful solution when you frequently query a subset of data from a large table.

Consider the following characteristics of filtered indexes:
- They are defined with a filter predicate to specify the conditions for including or excluding rows.
- They are created on a subset of rows that match the filter criteria.
- They can improve query performance by narrowing down the search space.
- They reduce index maintenance overhead by excluding unnecessary data.

## Conclusion

In summary, the main difference between a non-clustered index and a filtered index is that a non-clustered index is created on all rows of a table, while a filtered index is created on a subset of rows that satisfy a specified filter predicate. Understanding these differences can help you choose the appropriate index type based on your specific database optimization needs.

#Database #Indexes