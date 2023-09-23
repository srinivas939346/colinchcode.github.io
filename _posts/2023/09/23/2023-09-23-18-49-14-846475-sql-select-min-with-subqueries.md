---
layout: post
title: "SQL SELECT min with subqueries"
description: " "
date: 2023-09-23
tags: [Subqueries]
comments: true
share: true
---

In SQL, the `MIN` function retrieves the minimum value from a column in a table. When working with more complex queries, you might need to use subqueries to achieve the desired result. Subqueries allow you to perform queries within queries, providing more flexibility and control.

## Basic Syntax of SQL SELECT MIN

The basic syntax to retrieve the minimum value from a column in a table is as follows:

```sql
SELECT MIN(column_name) FROM table_name;
```

Let's say we have a `products` table with the following structure:

| id | name       | price |
|----|------------|-------|
| 1  | Laptop     | 800   |
| 2  | Smartphone | 700   |
| 3  | Tablet     | 500   |

To find the minimum price from the `products` table, we can use the following query:

```sql
SELECT MIN(price) FROM products;
```

This will return `500` as the minimum price.

## Using Subqueries to SELECT MIN

Subqueries can be used to perform more advanced queries. Let's take an example where we want to find the product with the minimum price from the `products` table.

```sql
SELECT name, price
FROM products
WHERE price = (SELECT MIN(price) FROM products);
```

In this query, the subquery `(SELECT MIN(price) FROM products)` is used to find the minimum price. The outer query then filters the products with this minimum price.

The result of the above query will be:

| name       | price |
|------------|-------|
| Tablet     | 500   |

The subquery `(SELECT MIN(price) FROM products)` returns `500`, and the outer query filters the rows with a price of `500`, giving us the product with the minimum price.

## Conclusion

Using subqueries with the `MIN` function in SQL allows us to perform more complex queries to retrieve the minimum value from a column. It provides greater flexibility and control in extracting the desired information from a table.

#SQL #Subqueries