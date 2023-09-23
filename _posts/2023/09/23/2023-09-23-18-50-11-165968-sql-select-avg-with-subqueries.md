---
layout: post
title: "SQL SELECT avg with subqueries"
description: " "
date: 2023-09-23
tags: [subqueries]
comments: true
share: true
---

In SQL, the AVG function is used to calculate the average value of a column. It is often useful to perform the average calculation based on specific subquery results. This can be achieved by using subqueries within the AVG function.

## Syntax

The syntax for using AVG with subqueries is as follows:

```sql
SELECT AVG(subquery_column)
FROM (subquery)
```

## Example

Let's consider a hypothetical scenario where we have a table called "sales" with the following columns: "product_id", "sales_amount", and "city". We want to calculate the average sales amount for each city.

```sql
SELECT city, AVG(sales_amount)
FROM sales
GROUP BY city
```

To further enhance the above query, let's assume we only want to include cities where the average sales amount is greater than a certain threshold. We can achieve this by using a subquery.

```sql
SELECT city, AVG(sales_amount)
FROM sales
WHERE city IN (
  SELECT city
  FROM sales
  GROUP BY city
  HAVING AVG(sales_amount) > 1000
)
GROUP BY city
```

In the above example, the subquery is used to filter out cities whose average sales amount is less than 1000. The outer query then calculates the average sales amount for the remaining cities.

By using subqueries within the AVG function, we can perform complex calculations and derive meaningful insights from our data.

#sql #subqueries