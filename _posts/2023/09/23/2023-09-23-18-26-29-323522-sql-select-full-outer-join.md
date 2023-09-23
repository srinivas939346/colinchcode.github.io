---
layout: post
title: "SQL SELECT full outer join"
description: " "
date: 2023-09-23
tags: [join]
comments: true
share: true
---
title: SQL SELECT Full Outer Join
description: Learn how to use the full outer join in SQL to combine data from two tables.
tags: SQL, join
---

# SQL SELECT Full Outer Join

In SQL, a **full outer join** allows you to combine data from two tables, including all rows from both tables, regardless of whether they have a matching row in the other table. It is useful when you want to include all records from both tables in the result set.

The syntax for performing a full outer join in SQL is as follows:

```sql
SELECT column1, column2, ...
FROM table1
FULL OUTER JOIN table2
ON table1.column_name = table2.column_name;
```

Here's an example to illustrate how a full outer join works:

Suppose we have two tables - `customers` and `orders`. The `customers` table holds information about customers, and the `orders` table holds information about orders placed by customers. 

Let's perform a full outer join between these two tables to get a result set with all customers and their corresponding orders, including those who have not placed any orders yet:

```sql
SELECT customers.customer_id, customers.customer_name, orders.order_id, orders.order_date
FROM customers
FULL OUTER JOIN orders
ON customers.customer_id = orders.customer_id;
```

In this example, the `customer_id` column is used as the common column to join the tables.

Remember that a full outer join returns all rows from both tables, regardless of the matching rows. If there is no match, NULL values will be returned for the columns of the table that does not have a matching row.

By using the full outer join, you can easily combine data from two tables and include all records from both tables in the result set.

**#SQL, #join**