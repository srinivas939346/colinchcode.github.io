---
layout: post
title: "Using SQL AVG with JOIN clause for combining tables"
description: " "
date: 2023-09-24
tags: []
comments: true
share: true
---

In SQL, the `AVG` function is used to calculate the average value of a column in a table. In scenarios where you need to combine multiple tables, you can use the `JOIN` clause to fetch data from different tables based on a common column or key.

Let's see an example where we want to calculate the average rating of a product based on the ratings given in one table and the product details stored in another table.

## Tables structure

**Table: products**

| product_id | name       | price |
|------------|------------|-------|
| 1          | Product 1  | 10.99 |
| 2          | Product 2  | 15.99 |
| 3          | Product 3  | 20.99 |

**Table: ratings**

| rating_id | product_id | rating |
|-----------|------------|--------|
| 1         | 1          | 4.5    |
| 2         | 1          | 3.9    |
| 3         | 2          | 5.0    |
| 4         | 3          | 4.8    |
| 5         | 3          | 4.2    |

## SQL Query

To calculate the average rating of products, we can use the `AVG` function in combination with the `JOIN` clause. Here's an example query:

```sql
SELECT products.product_id, products.name, AVG(ratings.rating) AS average_rating
FROM products
JOIN ratings ON products.product_id = ratings.product_id
GROUP BY products.product_id, products.name;
```

Let's analyze the query step by step:

1. We specify the columns we want to select: `products.product_id`, `products.name`, and the average rating using the `AVG(ratings.rating)` function.
2. We specify the tables we want to join: `products` table with `ratings` table using the common column `product_id`.
3. We group the result by `products.product_id` and `products.name` to ensure we get the average rating for each individual product.
4. Finally, we execute the query and retrieve the average ratings for each product.

The expected result of the query would be:

| product_id | name      | average_rating |
|------------|-----------|----------------|
| 1          | Product 1 | 4.2            |
| 2          | Product 2 | 5.0            |
| 3          | Product 3 | 4.5            |

In conclusion, by combining the `AVG` function and `JOIN` clause, you can accurately calculate the average value of a column from multiple tables in SQL.