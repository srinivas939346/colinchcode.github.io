---
layout: post
title: "SQL SELECT aggregate with where"
description: " "
date: 2023-09-23
tags: [Aggregate]
comments: true
share: true
---

Let's say we have a table called "sales" with the following structure:

```sql
CREATE TABLE sales (
    id INT,
    item VARCHAR(50),
    quantity INT,
    price DECIMAL(10,2)
);
```

To demonstrate how to use an aggregate function with a WHERE clause, let's find the total quantity of a specific item where the price is greater than a certain value. We'll use the SUM() function to calculate the total quantity.

```sql
SELECT item, SUM(quantity) AS total_quantity
FROM sales
WHERE price > 100
GROUP BY item;
```

In the above example, we are selecting the "item" column and calculating the sum of the "quantity" column using the SUM() function. The result is aliased as "total_quantity" for better readability. The WHERE clause is used to filter the rows based on the condition "price > 100". Finally, we are grouping the results by the "item" column using the GROUP BY clause.

This query will give us the total quantity of each item where the price is greater than 100. You can replace the table name, column names, and condition with your specific requirements.

Remember to adjust the table structure, column names, and condition based on your own database schema and data.

#SQL #Aggregate