---
layout: post
title: "Calculating the rolling average in SQL using AVG function"
description: " "
date: 2023-09-24
tags: [rollingaverage]
comments: true
share: true
---

In SQL, calculating the rolling average can be achieved using the AVG function along with the window function feature. 

## Understanding the AVG function and Window Functions

The AVG function is a built-in function in SQL that calculates the average value of a column. It takes a column as input and returns the average value.

Window functions, on the other hand, perform calculations across a set of rows that are somehow related to the current row. They are used in conjunction with the OVER() clause to define the window or set of rows over which the calculation is done.

## Syntax for Calculating the Rolling Average

The syntax for calculating the rolling average using the AVG function and window functions in SQL is as follows:

```sql
SELECT column_name, AVG(column_name) OVER (ORDER BY order_column ROWS n PRECEDING) as rolling_average
FROM table_name
```

In the above syntax:

- `column_name` is the name of the column for which you want to calculate the rolling average.
- `order_column` is the column used to order the rows.
- `n` is the number of preceding rows to include in the average calculation. Change this value to adjust the window size.

## Example Usage

Let's assume we have a table called `sales` with two columns: `date` and `revenue`. We want to calculate the rolling average of revenue over a window of the previous 7 days.

Here's an example query that calculates the rolling average:

```sql
SELECT date, revenue, AVG(revenue) OVER (ORDER BY date ROWS 7 PRECEDING) as rolling_average
FROM sales
```

The above query will return the date, revenue, and rolling average columns. The rolling average column will contain the average revenue for the previous 7 days for each row.

## Conclusion

Calculating the rolling average in SQL is made possible by the AVG function and window functions. By using the OVER() clause with appropriate ordering and window size, you can easily calculate the rolling average for any column in your database table.

#sql #rollingaverage