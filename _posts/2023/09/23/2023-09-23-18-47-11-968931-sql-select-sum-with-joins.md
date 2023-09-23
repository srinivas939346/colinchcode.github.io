---
layout: post
title: "SQL SELECT sum with joins"
description: " "
date: 2023-09-23
tags: [Join]
comments: true
share: true
---

Let's consider a database scenario with two tables: `orders` and `order_items`. The `orders` table contains information about the orders, such as order ID and customer ID, while the `order_items` table contains information about the items in each order, such as item ID, order ID, and quantity.

To calculate the sum of the quantities for all the items in each order, we can use the `SUM` function along with the `JOIN` clause. Here's an example of how to write the SQL query for it:

```sql
SELECT o.order_id, SUM(oi.quantity) AS total_quantity
FROM orders o
JOIN order_items oi ON o.order_id = oi.order_id
GROUP BY o.order_id;
```

In the above query, we are selecting the `order_id` from the `orders` table and calculating the sum of the `quantity` column from the `order_items` table using the `SUM` function. 

The `JOIN` condition specifies how the two tables are related, in this case, matching the `order_id` column from both tables. The `GROUP BY` clause groups the result by the `order_id`, which allows us to calculate the sum for each order.

The result of this query will provide the order ID along with the total quantity of items in each order.

By using joins and the `SUM` function, you can easily perform calculations on related data from multiple tables in SQL. It's a powerful way to aggregate data and extract valuable insights from your database.

#SQL #Join #Sum