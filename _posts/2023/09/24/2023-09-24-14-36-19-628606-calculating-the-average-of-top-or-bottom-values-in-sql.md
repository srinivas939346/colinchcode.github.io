---
layout: post
title: "Calculating the average of top or bottom values in SQL"
description: " "
date: 2023-09-24
tags: [Conclusion, DataAnalysis]
comments: true
share: true
---

In SQL, you can calculate the average of the top or bottom values in a table using the `TOP` or `LIMIT` clause to select the desired number of records, and then applying the `AVG` function on the selected records.

Here's an example of how you can calculate the average of the top or bottom values in a table in SQL:

## Calculating the Average of Top Values

Let's say we have a table called `sales` with columns `product_name` and `amount_sold`. We want to calculate the average amount sold for the top 5 products with the highest sales. 
```sql
SELECT AVG(amount_sold) AS average_sales
FROM (
  SELECT TOP 5 amount_sold
  FROM sales
  ORDER BY amount_sold DESC
) AS top_sales;
```

In this example, we use a subquery to select the top 5 `amount_sold` values from the `sales` table and then calculate the average of those sales using the `AVG` function.

## Calculating the Average of Bottom Values

Now, let's consider a scenario where we want to calculate the average amount sold for the bottom 10 products. 
```sql
SELECT AVG(amount_sold) AS average_sales
FROM (
  SELECT amount_sold
  FROM sales
  ORDER BY amount_sold ASC
  LIMIT 10
) AS bottom_sales;
```

Here, we modify the query to select the bottom 10 `amount_sold` values by using the `LIMIT` clause with the `ASC` sorting order. Once again, we calculate the average of the selected sales using the `AVG` function.

#Conclusion

Calculating the average of the top or bottom values in SQL is straightforward. Use the `TOP` or `LIMIT` clause to select the desired number of records and then apply the `AVG` function to calculate the average value. By leveraging these SQL features, you can easily analyze and make informed decisions based on the top or bottom values in your data.

#SQL #DataAnalysis