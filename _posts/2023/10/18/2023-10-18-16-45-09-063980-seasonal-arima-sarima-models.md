---
layout: post
title: "[python] Seasonal ARIMA (SARIMA) models"
description: " "
date: 2023-10-18
tags: [python]
comments: true
share: true
---

Seasonal ARIMA (SARIMA) models are a extension of the basic ARIMA models that take into account seasonality in time series data. These models are widely used in fields such as economics, finance, and meteorology, where seasonal patterns are prevalent.

## Understanding Seasonal ARIMA models

ARIMA stands for Autoregressive Integrated Moving Average. It is a time series forecasting model that combines autoregressive (AR), moving average (MA), and differencing (I) components to capture the linear dependencies and trends in the data.

In a seasonal ARIMA model, the seasonal component is added to the ARIMA model to handle cyclic patterns that occur at fixed intervals, such as daily, weekly, or monthly.

The seasonal component of a SARIMA model consists of an additional set of AR, MA, and differencing terms, which capture the seasonal patterns in the data. These terms are similar to the non-seasonal ARIMA model, but they operate on the seasonal lags.

The general notation for a seasonal ARIMA model is SARIMA(p, d, q)(P, D, Q)s, where:

- **p, d, q**: the non-seasonal AR, differencing, and MA orders, respectively.
- **P, D, Q**: the seasonal AR, differencing, and MA orders, respectively.
- **s**: the length of the seasonal cycle.

## Fitting a Seasonal ARIMA model

To fit a seasonal ARIMA model to a time series, you can use libraries like `statsmodels` in Python. Here's an example code snippet that demonstrates fitting a SARIMA model to a time series:

```python
import statsmodels.api as sm

# Create SARIMA model
model = sm.tsa.SARIMAX(data, order=(p, d, q), seasonal_order=(P, D, Q, s))

# Fit the model
result = model.fit()

# Print summary of the model
print(result.summary())
```

In this code, `data` represents the time series data, while `p, d, q, P, D, Q, s` are the order parameters for the seasonal ARIMA model. The `SARIMAX` class from `statsmodels` is used to create the SARIMA model, and the `fit()` method is called to estimate the model parameters.

The `result.summary()` method provides a summary of the fitted SARIMA model, including the estimated coefficients, standard errors, p-values, and other statistical information.

## Forecasting with Seasonal ARIMA models

Once a SARIMA model is fitted to a time series, you can use it to make forecasts. The `forecast()` method in `statsmodels` can be used to generate future predictions based on the fitted model.

Here's an example code snippet that demonstrates how to use the SARIMA model for forecasting:

```python
# Generate forecast
forecast = result.forecast(steps=N)

# Print forecasted values
print(forecast)
```

In this code, `result` represents the fitted SARIMA model obtained from the previous step. The `forecast()` method is called with `steps=N` to generate N future predictions. The resulting forecasted values are then printed.

## Conclusion

Seasonal ARIMA (SARIMA) models are powerful tools for time series forecasting, particularly when dealing with data that exhibits seasonal patterns. By incorporating seasonal components into the ARIMA model, SARIMA models can better capture and predict cyclic patterns that occur at fixed intervals.