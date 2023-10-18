---
layout: post
title: "[python] Handling seasonality in ARIMA models with Fourier series"
description: " "
date: 2023-10-18
tags: [python]
comments: true
share: true
---

Seasonality is a common pattern observed in time series data, where the values tend to exhibit regular fluctuations over a fixed period. When building time series models such as ARIMA (AutoRegressive Integrated Moving Average), it is important to account for seasonality in order to make accurate predictions.

ARIMA models are well-suited to handle non-seasonal time series data, but they struggle with capturing seasonal patterns. One way to address this issue is by using Fourier series to model and remove the seasonality component from the data before fitting an ARIMA model.

## What is a Fourier Series?

A Fourier series is a mathematical representation of a periodic function as a sum of sine and cosine functions with different frequencies. It is widely used in various fields, including signal processing and time series analysis.

In the context of time series modeling, a Fourier series can be applied to decompose the data into its various frequency components, including the seasonal component. By representing the seasonal variation as a sum of sine and cosine functions, we can effectively remove the seasonality from the data.

## Steps to Handle Seasonality with Fourier Series in ARIMA Models

To handle seasonality in ARIMA models using Fourier series, follow these steps:

1. Decompose the time series: Start by decomposing the time series data into its trend, seasonality, and residual components using methods like Seasonal Decomposition of Time Series (STL) or moving averages.

2. Differencing: If the data has a trend component, apply differencing to make it stationary. Differencing involves subtracting the previous observation from the current observation.

3. Fourier series analysis: Apply a Fourier series analysis to the seasonal component of the time series. This involves fitting a Fourier regression model to identify the frequencies and amplitudes of the seasonal components.

4. Remove seasonal component: Subtract the seasonal component obtained from the Fourier series analysis from the original time series data to remove the seasonality.

5. Fit ARIMA model: Finally, fit an ARIMA model to the deseasonalized data to capture the remaining non-seasonal patterns and make predictions.

## Example Code

Here's an example of how to handle seasonality in ARIMA models using Fourier series in Python:

```python
import pandas as pd
import numpy as np
import statsmodels.api as sm
from statsmodels.tsa.arima.model import ARIMA

# Load time series data
data = pd.read_csv('time_series_data.csv')

# Decompose time series
decomposition = sm.tsa.seasonal_decompose(data['value'], period=12)
trend = decomposition.trend
seasonal = decomposition.seasonal
residual = decomposition.resid

# Differencing
differenced_data = data['value'].diff().dropna()

# Fourier series analysis
fourier = sm.tsa.statespace.tools.ccffilter(seasonal, np.arange(1, 10))

# Remove seasonal component
deseasonalized_data = data['value'] - fourier.filtered_state[0]

# Fit ARIMA model
model = ARIMA(deseasonalized_data, order=(1, 0, 1))
model_fit = model.fit()

# Make predictions
predictions = model_fit.predict(start=len(data), end=len(data)+n)
```

In this example, we load the time series data and decompose it into its trend, seasonal, and residual components using the `seasonal_decompose` function from the `statsmodels` library. We then apply differencing to remove the trend component and perform a Fourier series analysis on the seasonal component. Finally, we remove the seasonal component from the original data and fit an ARIMA model to make predictions.

## Conclusion

Handling seasonality in ARIMA models is crucial for accurate time series forecasting. By using Fourier series to decompose and remove the seasonal component, we can greatly improve the performance of ARIMA models. This approach allows us to capture both the non-seasonal and seasonal patterns in the data, leading to more reliable predictions.