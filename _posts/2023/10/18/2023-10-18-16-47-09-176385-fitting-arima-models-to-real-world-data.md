---
layout: post
title: "[python] Fitting ARIMA models to real-world data"
description: " "
date: 2023-10-18
tags: [python]
comments: true
share: true
---

ARIMA (Autoregressive Integrated Moving Average) models are widely used in time series analysis to forecast future values based on past observations. In this blog post, we'll explore how to fit ARIMA models to real-world data in Python, using the `statsmodels` library.

## Table of Contents
1. Introduction to ARIMA models
2. Stationarity and differencing
3. Model selection: AIC and BIC
4. Fitting an ARIMA model
5. Evaluating model performance
6. Forecasting future values
7. Conclusion

## 1. Introduction to ARIMA models

ARIMA models combine the autoregressive (AR), moving average (MA), and differencing (I) components to model the underlying patterns in a time series. The AR component captures the dependency between an observation and a certain number of lagged observations, the MA component models the error terms as a linear combination of past error terms, and the I component handles non-stationarity by differencing the observations.

## 2. Stationarity and differencing

Before fitting an ARIMA model, it is essential to ensure that the time series is stationary. Stationarity implies that the mean, variance, and autocovariance structure of the series do not change over time. If the series is non-stationary, differencing can be applied to achieve stationarity.

## 3. Model selection: AIC and BIC

ARIMA models can have different combinations of AR, MA, and I components. To determine the optimal model, we can use the Akaike Information Criterion (AIC) and Bayesian Information Criterion (BIC). These criteria measure the trade-off between model goodness-of-fit and complexity, helping us select the model with the best balance.

## 4. Fitting an ARIMA model

To fit an ARIMA model in Python, we can utilize the `ARIMA` class provided by the `statsmodels` library. The `ARIMA` class allows us to specify the order of the AR, I, and MA components and provides methods to estimate the model parameters.

```python
import numpy as np
import pandas as pd
import statsmodels.api as sm

# Load and preprocess data
data = pd.read_csv('data.csv')
data['date'] = pd.to_datetime(data['date'])
data.set_index('date', inplace=True)

# Fit ARIMA model
model = sm.tsa.ARIMA(data, order=(2,1,1))
results = model.fit()

# Print model summary
print(results.summary())
```

## 5. Evaluating model performance

After fitting the ARIMA model, it is crucial to evaluate its performance to assess its accuracy in predicting future values. Common evaluation techniques include calculating the Mean Absolute Error (MAE), Root Mean Squared Error (RMSE), and plotting the residuals.

## 6. Forecasting future values

Once we have a fitted ARIMA model, we can use it to forecast future values of the time series. We can achieve this by utilizing the `get_forecast` method provided by the `ARIMAResults` class.

```python
# Forecast future values
forecast = results.get_forecast(steps=10)
future_dates = pd.date_range(start=data.index[-1], periods=10, freq='D')

# Print forecasted values
print(forecast.summary())
print(forecast.predicted_mean)
print(future_dates)
```

## 7. Conclusion

In this blog post, we learned how to fit ARIMA models to real-world data. We covered the importance of stationarity, model selection using AIC and BIC, fitting the ARIMA model in Python, evaluating model performance, and forecasting future values. ARIMA models are powerful tools for time series analysis, and with the `statsmodels` library in Python, fitting and forecasting becomes straightforward. Always remember to assess the model performance and validate the results against real-world observations.