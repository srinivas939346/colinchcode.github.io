---
layout: post
title: "[python] Forecasting with multiple seasonal patterns using SARIMA"
description: " "
date: 2023-10-18
tags: [python]
comments: true
share: true
---

Time series data often exhibit multiple seasonal patterns, which can pose challenges when trying to forecast future values. One widely used method for tackling this issue is SARIMA (Seasonal Autoregressive Integrated Moving Average) modeling. In this blog post, we will explore how to use SARIMA to forecast time series data with multiple seasonal patterns using Python.

### What is SARIMA?

SARIMA is an extension of the classic ARIMA model that takes into account seasonal patterns in the data. It consists of three main components: the autoregressive (AR) component, the differencing (I) component, and the moving average (MA) component. The seasonal part of SARIMA adds an additional set of AR, differencing, and MA terms to capture the seasonal patterns.

### Data Preparation

Let's start by loading the required libraries and importing our time series data.

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.statespace.sarimax import SARIMAX

# Load the time series data
data = pd.read_csv('data.csv', index_col=0, parse_dates=True)
```

Next, we need to make sure that the data is suitable for SARIMA modeling. This involves checking for stationarity, transforming the data if necessary, and identifying the seasonal period.

### Model Selection

The next step is to determine the appropriate SARIMA model for our data. This involves selecting the order of the AR, I, and MA components, as well as the seasonal order. One way to do this is by using the auto_arima function from the pmdarima library.

```python
from pmdarima import auto_arima

# Find the best SARIMA model using auto_arima
model = auto_arima(data, seasonal=True, m=7)
order = model.order
seasonal_order = model.seasonal_order
```

The `auto_arima` function automatically selects the best SARIMA model based on the AIC (Akaike Information Criterion) score. We specify `seasonal=True` and the seasonal period `m` to enable the detection of multiple seasonal patterns.

### Model Training and Forecasting

Once we have selected the appropriate SARIMA model, we can proceed to train the model and make predictions.

```python
# Train the SARIMA model
model = SARIMAX(data, order=order, seasonal_order=seasonal_order)
model_fit = model.fit()

# Forecast future values
future = model_fit.get_forecast(steps=30)
forecast = future.predicted_mean
```

The `SARIMAX` class from the statsmodels library is used to define and fit the SARIMA model. We pass the selected order and seasonal order to the model and call the `fit` method to train the model on our data.

Once the model is trained, we can use the `get_forecast` method to generate forecasts for future time periods. In this example, we are forecasting 30 steps ahead.

### Visualizing the Forecast

Finally, let's visualize the forecasted values along with the actual data.

```python
# Plot the actual data and forecasted values
plt.plot(data, label='Actual')
plt.plot(forecast, label='Forecast')
plt.xlabel('Date')
plt.ylabel('Value')
plt.legend()
plt.show()
```

By plotting the actual data and the forecasted values on the same graph, we can evaluate the performance of our SARIMA model visually.

### Conclusion

In this blog post, we learned how to use SARIMA to forecast time series data with multiple seasonal patterns. SARIMA is a powerful tool for handling complex time series data and can be easily implemented in Python using the statsmodels library.