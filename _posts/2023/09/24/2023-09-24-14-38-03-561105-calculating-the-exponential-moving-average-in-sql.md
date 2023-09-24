---
layout: post
title: "Calculating the exponential moving average in SQL"
description: " "
date: 2023-09-24
tags: [ExponentialMovingAverage]
comments: true
share: true
---

Exponential Moving Average (EMA) is a commonly used statistical calculation in finance and time series analysis. It gives more weight to recent data points while progressively reducing the impact of older data points. In this blog post, we will explore how to calculate the EMA using SQL.

Before we dive into the code, let's understand the formula for calculating the EMA. The EMA calculation is recursive and requires an initial value called the EMA seed. The general formula for calculating the EMA is as follows:

```
EMA(current) = ((current - EMA(prev)) * smoothing constant) + EMA(prev)
```

Here, the smoothing constant determines the weight given to the current data point. It is typically calculated based on the desired time period or window size.

Now, let's proceed with an example to calculate the EMA for a given dataset using SQL.

## Create a Table and Seed Data

Let's assume we have a table called `stock_prices` with the following schema:

```sql
CREATE TABLE stock_prices (
  id INT PRIMARY KEY,
  symbol VARCHAR(10),
  price DECIMAL(10, 2),
  date DATE
);
```

To calculate the EMA, we need a few rows of seed data. Here's an example of how you can insert some sample data into the table:

```sql
INSERT INTO stock_prices (id, symbol, price, date)
VALUES
  (1, 'AAPL', 100.00, '2022-01-01'),
  (2, 'AAPL', 105.50, '2022-01-02'),
  (3, 'AAPL', 102.75, '2022-01-03'),
  (4, 'AAPL', 108.20, '2022-01-04'),
  (5, 'AAPL', 106.50, '2022-01-05');
```

## Calculating the EMA

To calculate the EMA in SQL, we can use a recursive CTE (Common Table Expression) and a series of self-joins. Here's an example query that calculates the EMA for the `AAPL` stock symbol with a smoothing constant of 0.5:

```sql
WITH recursive ema_cte AS (
  SELECT
    id,
    symbol,
    price,
    date,
    price AS ema
  FROM
    stock_prices
  WHERE
    symbol = 'AAPL'
    AND date = '2022-01-01'
  UNION ALL
  SELECT
    sp.id,
    sp.symbol,
    sp.price,
    sp.date,
    ((sp.price - ema_cte.ema) * 0.5) + ema_cte.ema AS ema
  FROM
    stock_prices sp
    JOIN ema_cte ON sp.date = ema_cte.date + INTERVAL '1 DAY'
)
SELECT
  id,
  symbol,
  price,
  date,
  ema
FROM
  ema_cte;
```

In this query, we start with the seed data as the initial EMA value (`price`). Then, we recursively join the `stock_prices` table with the CTE to calculate the EMA for each subsequent date.

## Conclusion

Calculating the Exponential Moving Average in SQL can be accomplished using recursive CTEs and self-joins. By understanding the EMA formula and leveraging SQL's capabilities, we can effectively analyze time series data.

#SQL #ExponentialMovingAverage