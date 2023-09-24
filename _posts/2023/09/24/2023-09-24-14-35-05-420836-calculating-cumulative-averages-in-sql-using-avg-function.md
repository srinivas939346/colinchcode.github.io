---
layout: post
title: "Calculating cumulative averages in SQL using AVG function"
description: " "
date: 2023-09-24
tags: [WindowFunctions]
comments: true
share: true
---

Here's an example of how to calculate cumulative averages using the AVG function in SQL:

```sql
SELECT
   value,
   AVG(value) OVER (ORDER BY date ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS cumulative_avg
FROM
   your_table;
```

Let's break down the query:

1. `SELECT value`: Select the value column from your table.

2. `AVG(value) OVER (ORDER BY date ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)`: Use the AVG function with the OVER clause to calculate the average. The `ORDER BY date` specifies the order in which the calculation is performed, and the `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` indicates that the average should be calculated from the beginning of the table up to the current row.

3. `AS cumulative_avg`: Alias the calculated value as "cumulative_avg" to make it clear what the column represents.

4. `FROM your_table`: Specify the table name where the data is stored. Replace `your_table` with the actual name of your table.

This query will return the original value column along with a new column called cumulative_avg, which represents the cumulative average up to each row.

#SQL #WindowFunctions