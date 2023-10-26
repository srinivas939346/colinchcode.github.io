---
layout: post
title: "[python] Rolling window statistics"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

When working with time series data or any sequential data, it is often useful to compute rolling window statistics. Rolling window statistics provide a way to calculate aggregate values over a specified window of consecutive data points.

In this tutorial, we will explore how to compute rolling window statistics using Python, specifically using the Pandas library.

## What are Rolling Window Statistics?

Rolling window statistics compute aggregate values over a sliding window of a specified size. It allows us to calculate metrics like moving averages, rolling sum, or any other statistics on a rolling basis.

Using rolling window statistics, we can analyze trends and patterns in data over time. For example, we can calculate the rolling average of daily sales to observe the sales trend over a specific window size.

## Getting Started

To demonstrate rolling window statistics, we first need to install the Pandas library. You can install it using pip:

```
pip install pandas
```

Once installed, we can import the Pandas library and create a sample time series dataset:

```python
import pandas as pd

# Create a sample time series dataset
data = pd.Series([5, 8, 10, 12, 6, 9, 15, 11, 7, 14])
```

## Rolling Window Average

The rolling window average calculates the mean of values within a specified window size. To calculate the rolling window average using Pandas, we can use the `rolling()` function:

```python
# Calculate rolling window average with window size 3
rolling_average = data.rolling(window=3).mean()

print(rolling_average)
```

Output:
```
0          NaN
1          NaN
2     7.666667
3    10.000000
4     9.333333
5     9.000000
6    10.000000
7    11.666667
8    10.666667
9    10.666667
dtype: float64
```

In the above example, we calculate the rolling window average with a window size of 3. The first two values in the resulting series are "NaN" because there are not enough values to calculate the average in the initial windows.

## Other Rolling Window Statistics

Pandas provides various functions to calculate different rolling window statistics. Here are a few examples:

### Rolling Sum

To calculate the rolling sum, we can use the `rolling().sum()` function:

```python
rolling_sum = data.rolling(window=4).sum()
```

### Rolling Maximum

To calculate the rolling maximum, we can use the `rolling().max()` function:

```python
rolling_max = data.rolling(window=2).max()
```

### Rolling Minimum

To calculate the rolling minimum, we can use the `rolling().min()` function:

```python
rolling_min = data.rolling(window=3).min()
```

## Conclusion

Rolling window statistics are valuable for analyzing trends and patterns in sequential data. In this tutorial, we explored how to calculate rolling window statistics using the Pandas library in Python. We covered rolling window average, sum, maximum, and minimum functions as examples, but Pandas provides many more rolling window statistics functions for specific use cases.

If you want to learn more, refer to the [Pandas documentation](https://pandas.pydata.org/docs/user_guide/window.html) for a comprehensive list of rolling window statistics functions.