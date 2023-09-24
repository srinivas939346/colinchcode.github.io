---
layout: post
title: "Using SQL AVG with CASE statement for conditional averages"
description: " "
date: 2023-09-24
tags: [CASE]
comments: true
share: true
---

In SQL, the **AVG()** function is commonly used to calculate the average value of a column. However, there are cases where you might need to calculate conditional averages based on certain criteria. This is where the **CASE** statement comes into play.

The **CASE** statement in SQL allows you to perform conditional logic within your query. By combining it with the **AVG()** function, you can calculate different averages based on specific conditions.

Let's consider the following scenario: you have a table called `sales` which contains information about sales transactions. Each row in the table represents a sale, and it includes columns such as `product`, `quantity`, and `price`.

To calculate the average price for each product, you can utilize the **CASE** statement within the **AVG()** function as follows:

```sql
SELECT 
   product,
   AVG(CASE 
         WHEN price > 0 THEN price 
         ELSE 0 
       END) AS average_price
FROM sales
GROUP BY product;
```

In this example, we use the **CASE** statement to check if the price is greater than 0. If it is, we include the price in the calculation of the average. Otherwise, we set the value to 0.

The **AVG()** function then calculates the average of the conditional values for each product and returns the result as the `average_price` column in the result set.

By using the **CASE** statement within the **AVG()** function, you can easily calculate conditional averages based on your specific requirements. This approach provides flexibility and allows you to perform complex calculations on your data.

Using the **AVG()** function with the **CASE** statement is just one example of how you can leverage SQL's powerful capabilities to manipulate and analyze your data. Understanding this concept can greatly enhance your ability to work with conditional averages and other similar calculations in SQL.

Give it a try in your next SQL query to calculate conditional averages based on your specific criteria!

#SQL #AVG #CASE