---
layout: post
title: "[python] Differencing in ARIMA models"
description: " "
date: 2023-10-18
tags: [python]
comments: true
share: true
---

In time series analysis, differencing is a common technique used to make a series stationary. Stationarity is important because many time series models, such as ARIMA (Autoregressive Integrated Moving Average), assume that the data has constant mean and variance over time. 

ARIMA models consist of three components: autoregressive (AR), integrated (I), and moving average (MA). The integrated component in ARIMA accounts for differencing the data to achieve stationarity.

## Why do we need to difference the data?

Non-stationary data can exhibit trends and seasonality, which makes it difficult to make reliable predictions. By differencing the data, we can transform a non-stationary series into a stationary one, making it easier to model and forecast.

## First-order differencing

The simplest form of differencing is first-order differencing, denoted as `d=1`. First-order differencing calculates the difference between consecutive observations in a time series. This can be achieved in Python using the `diff()` function from the `pandas` library:

```python
import pandas as pd

# Assuming `data` is a pandas Series or DataFrame
# Perform first-order differencing
differenced_data = data.diff(periods=1)
```

The resulting `differenced_data` will have one less observation than the original data, as the first observation is eliminated due to differencing.

## Higher-order differencing

If the first-order differenced data still exhibits non-stationarity, higher-order differencing can be applied. Higher-order differencing involves performing first-order differencing multiple times until the desired level of stationarity is achieved.

```python
import pandas as pd

# Assuming `data` is a pandas Series or DataFrame
# Perform second-order differencing
differenced_data = data.diff(periods=1)

# Perform third-order differencing
differenced_data = differenced_data.diff(periods=1)

# Continue differencing if necessary
```

The number of times differencing is applied depends on the characteristics of the time series. It is important to note that overly differencing the data might result in loss of valuable information.

## Assessing stationarity

To determine if differencing has achieved stationarity, we can perform statistical tests or visualize the data. Statistical tests such as the Augmented Dickey-Fuller (ADF) test can determine if a series is stationary or not.

```python
from statsmodels.tsa.stattools import adfuller

# Assuming `data` is a pandas Series or DataFrame
# Perform the ADF test
result = adfuller(data)

# Extract the p-value
p_value = result[1]

# Check if the series is stationary
if p_value < 0.05:
    print("The series is stationary.")
else:
    print("The series is non-stationary.")
```

Additionally, visualizing the time series and checking for clear trends or seasonality can also provide insights into the stationarity of the data.

## Conclusion

Differencing is an important step in preparing time series data for analysis using ARIMA models. By transforming a non-stationary series into a stationary one, we can leverage the power of ARIMA models to make accurate forecasts.