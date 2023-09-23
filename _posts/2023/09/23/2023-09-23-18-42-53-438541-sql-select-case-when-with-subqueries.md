---
layout: post
title: "SQL SELECT case when with subqueries"
description: " "
date: 2023-09-23
tags: [Subqueries]
comments: true
share: true
---

In SQL, the `CASE WHEN` statement can be combined with subqueries to perform complex conditional logic within a SELECT query. This powerful combination allows you to customize the result set based on various conditions.

Here's an example scenario where we want to retrieve a list of customers with their corresponding membership level based on their total purchase amount:

```sql
SELECT 
    customer_name,
    CASE 
        WHEN total_purchase_amount > 5000 THEN 'Gold'
        WHEN total_purchase_amount > 2000 THEN 'Silver'
        ELSE 'Bronze'
    END as membership_level
FROM (
    SELECT 
        customer_name,
        SUM(purchase_amount) as total_purchase_amount
    FROM 
        purchases
    GROUP BY 
        customer_name
) as subquery;
```

In this example, we have a table named `purchases` containing customer names and their corresponding purchase amounts. We use a subquery to calculate the total purchase amount for each customer.

Within the outer SELECT statement, the `CASE WHEN` statement is used to evaluate the total purchase amount for each customer and assign a membership level based on it. If the total purchase amount is greater than 5000, the membership level is 'Gold', if it's greater than 2000, the membership level is 'Silver', and for any other case, it is assigned 'Bronze'.

The result of the query will be a list of customer names along with their membership levels.

By combining the `CASE WHEN` statement with subqueries, you can perform complex conditional operations and derive meaningful insights from your data.

#SQL #Subqueries