---
layout: post
title: "How SQL HEAP works internally"
description: " "
date: 2023-09-23
tags: [SQLServer, HEAP]
comments: true
share: true
---

SQL HEAP, also known as SQL Server Heap, is a storage structure in a SQL Server database that stores data without any specific order. Unlike clustered or non-clustered indexes, the data in a HEAP is stored in an unordered structure known as a heap table.

## Understanding the Internal Working of SQL HEAP

When a table is created without a clustered index or a primary key, SQL Server creates a HEAP table to store the data. This means that there is no specific order to how the data is stored on disk. Each row of the table is identified by a unique identifier, known as a Row ID. The Row ID, along with the location of the data within the table, is stored in a separate allocation unit called the Index Allocation Map (IAM) page.

Here are the key points to understand about the internal working of SQL HEAP:

1. **Data Storage**:
   - Data is stored on data pages using a variable-length format.
   - Each data page is managed by the Page Free Space (PFS) page, which tracks the usage of the space on each data page.
   - The data is stored in the order it was inserted, without any specific sorting.

2. **Identifying Rows**:
   - Each row within the HEAP is identified by a Row ID.
   - The Row ID consists of a File ID, Page ID, and Slot ID.
   - The File ID identifies the physical file, the Page ID identifies the data page within the file, and the Slot ID identifies the slot within the data page where the row is located.

3. **Accessing Data**:
   - Since there is no specific order to the data in a HEAP, accessing data requires scanning the entire table.
   - This can result in slower read performance compared to tables with clustered indexes.
   - SQL Server uses a mechanism called "forwarded records" to handle updates that do not fit within the allocated space of a data page. In such cases, the updated record is moved to a new data page, and a forwarding pointer is left behind in the original location to redirect queries to the updated location.

## Conclusion

SQL HEAP provides a storage structure for tables in SQL Server where data is stored in an unordered manner. While it is useful for certain scenarios, it can result in slower read performance as compared to tables with clustered indexes. Understanding the internal workings of SQL HEAP can help in optimizing the database design and performance.

#SQL #SQLServer #HEAP #Database