---
layout: post
title: "Non-clustered index and hash indexes in SQL"
description: " "
date: 2023-09-22
tags: [indexing]
comments: true
share: true
---

In SQL, a non-clustered index is a data structure that enhances the performance of queries by providing quick access to specific columns or expressions. Unlike a clustered index, a non-clustered index does not determine the physical order of data in a table. Instead, it creates a separate structure that contains a copy of the indexed columns and a reference to the actual rows in the table.

When a query is executed, the database engine uses the non-clustered index to locate the rows that satisfy the search condition. It then retrieves the corresponding data using the pointer stored in the index.

Non-clustered indexes are useful for improving the performance of read operations such as SELECT queries. However, they come with some overhead as the index needs to be updated whenever the data in the table is modified (INSERT, UPDATE, DELETE). Therefore, it is important to carefully choose which columns to index and consider the tradeoff between the performance gain and the overhead of maintaining the index.

# Hash Indexes in SQL

Hash indexes are another type of index in SQL that is specifically designed for fast equality-based searches. They use a hash function to map the indexed column values to a hash table, where each entry consists of the indexed value and a pointer to the corresponding row.

When a query with an equality condition is executed, the hash index calculates the hash value of the search key and uses it to directly access the desired row or a small set of candidate rows. This type of index is particularly efficient for single-value lookups or exact matches.

Hash indexes are generally faster than non-clustered indexes for equality searches, but they are less effective for ranged queries or sorting. They also require a fixed amount of memory to store the hash table, which can limit their usefulness when working with large datasets.

Overall, the choice between non-clustered indexes and hash indexes depends on the specific use case and the types of queries executed against the database. Non-clustered indexes are more versatile and suitable for a wide range of queries, while hash indexes provide excellent performance for equality-based searches.

# #sql #indexing