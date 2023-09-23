---
layout: post
title: "SQL SELECT joins with different join types"
description: " "
date: 2023-09-23
tags: [JOIN]
comments: true
share: true
---

When working with SQL databases, it is common to combine data from multiple tables using JOIN operations. JOINs allow you to retrieve related data from different tables based on specified conditions. There are several types of JOIN operations available in SQL, each serving a different purpose. In this blog post, we will explore the most commonly used JOIN types in SQL Select statements.

## 1. INNER JOIN
The INNER JOIN is the most commonly used and default type of join in SQL. It returns only the rows that have matching values in both tables being joined. The syntax for an INNER JOIN is as follows:

```sql
SELECT *
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

## 2. LEFT JOIN
A LEFT JOIN returns all rows from the left table (table1) and the matching rows from the right table (table2). If there are no matching rows in the right table, NULL values are returned. The syntax for a LEFT JOIN is as follows:

```sql
SELECT *
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```

## 3. RIGHT JOIN
A RIGHT JOIN is the opposite of a LEFT JOIN. It returns all rows from the right table (table2) and the matching rows from the left table (table1). If there are no matching rows in the left table, NULL values are returned. The syntax for a RIGHT JOIN is as follows:

```sql
SELECT *
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```

## 4. FULL OUTER JOIN
A FULL OUTER JOIN returns all rows from both tables (table1 and table2) and includes NULL values for non-matching rows on either side. The syntax for a FULL OUTER JOIN varies depending on the database system you are using. Here's an example using the standard SQL syntax:

```sql
SELECT *
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

These are the basic JOIN types in SQL Select statements. Understanding and utilizing the appropriate JOIN type can help you retrieve data efficiently and accurately from multiple tables. Remember to choose the right JOIN type based on your specific requirements.

#SQL #JOIN