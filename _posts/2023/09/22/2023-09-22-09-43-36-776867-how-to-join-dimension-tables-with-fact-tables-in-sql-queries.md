---
layout: post
title: "How to join dimension tables with fact tables in SQL queries."
description: " "
date: 2023-09-22
tags: [Joins]
comments: true
share: true
---

When working with relational databases, it is common to have dimension tables and fact tables. Dimension tables contain descriptive attributes, such as product details or customer information, while fact tables contain numeric values or measures, such as sales data or quantities. In order to gain meaningful insights from your data, it is necessary to join these dimension tables with fact tables in your SQL queries. In this blog post, we will explore the different types of joins and how to use them effectively.

## Inner Join
The inner join is commonly used to combine values from both dimension and fact tables when there is a match between the join condition. It eliminates the unmatched records from both tables. Here is an example of using an inner join in an SQL query:

```sql
SELECT *
FROM dimension_table
INNER JOIN fact_table
ON dimension_table.key = fact_table.key;
```

In this example, `dimension_table` and `fact_table` are the names of the tables we want to join. `key` is the common column between these tables that we use to join them together. The result of this query will be a new table containing the joined records from both tables.

## Left Join
The left join is used when you want to retrieve all records from the left table (dimension table), along with matching records from the right table (fact table). In case there is no match, NULL values are returned for the columns of the right table. Here is an example of using a left join in an SQL query:

```sql
SELECT *
FROM dimension_table
LEFT JOIN fact_table
ON dimension_table.key = fact_table.key;
```

The result of this query will include all records from the `dimension_table`, along with corresponding records from the `fact_table` if a match is found. If no match is found, the columns of the `fact_table` will contain NULL values.

## Right Join
The right join is the opposite of the left join, where you retrieve all records from the right table (fact table), along with matching records from the left table (dimension table). In case there is no match, NULL values are returned for the columns of the left table. Here is an example of using a right join in an SQL query:

```sql
SELECT *
FROM dimension_table
RIGHT JOIN fact_table
ON dimension_table.key = fact_table.key;
```

The result of this query will include all records from the `fact_table`, along with corresponding records from the `dimension_table` if a match is found. If no match is found, the columns of the `dimension_table` will contain NULL values.

## Conclusion
Joining dimension tables with fact tables is a crucial part of analyzing data in relational databases. By using different types of joins, such as the inner join, left join, and right join, you can combine information from dimension tables with numerical data from fact tables to gain insights and make data-driven decisions.

#SQL #Joins