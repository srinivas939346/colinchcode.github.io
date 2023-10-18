---
layout: post
title: "[python] Hybrid models: combining ARIMA with other forecasting methods"
description: " "
date: 2023-10-18
tags: [python]
comments: true
share: true
---

When it comes to time series forecasting, ARIMA (AutoRegressive Integrated Moving Average) models are a popular choice due to their simplicity and ability to capture the trend and seasonality in data. However, ARIMA models may not always be the best option, especially when the data has complex patterns or outliers. In such cases, hybrid models that combine ARIMA with other forecasting methods can provide more accurate predictions.

Hybrid models typically work by using ARIMA to capture the underlying trend and seasonality in the data, and then using another forecasting method to handle the residuals or error term. This way, the strengths of both methods can be leveraged to improve the overall forecasting performance.

## Examples of Hybrid Models

### ARIMA with Exponential Smoothing

One popular hybrid model is combining ARIMA with exponential smoothing methods such as Holt-Winters. Exponential smoothing methods are well-suited for handling the residuals that ARIMA fails to capture. By combining the two methods, the hybrid model can effectively capture both the long-term trends and the short-term fluctuations in the data.

```python
import statsmodels.api as sm
from statsmodels.tsa.holtwinters import ExponentialSmoothing

# Fit ARIMA model
sarima_model = sm.tsa.SARIMAX(data, order=(p, d, q), seasonal_order=(P, D, Q, s)).fit()

# Get the residuals
residuals = sarima_model.resid

# Fit exponential smoothing model on the residuals
es_model = ExponentialSmoothing(residuals).fit()

# Combine the forecasts from both models
combined_forecast = sarima_model.predict(start, end) + es_model.predict(start, end)
```

### ARIMA with Machine Learning Models

Another approach is to combine ARIMA with machine learning models such as random forests or support vector machines. Machine learning models can often handle more complex patterns and nonlinear relationships in the data, which may be missed by ARIMA. By combining the two approaches, the hybrid model can capture both the temporal patterns and the underlying nonlinear relationships in the data.

```python
from sklearn.ensemble import RandomForestRegressor
import statsmodels.api as sm

# Fit ARIMA model
arima_model = sm.tsa.ARIMA(data, order=(p, d, q)).fit()

# Get the residuals
residuals = arima_model.resid

# Fit random forest model on the residuals
rf_model = RandomForestRegressor().fit(X, residuals)

# Combine the forecasts from both models
combined_forecast = arima_model.predict(start, end) + rf_model.predict(X_new)
```

### ARIMA with Neural Networks

Neural networks, specifically recurrent neural networks (RNNs), are another popular choice for capturing complex patterns in time series data. By combining ARIMA with RNNs, the hybrid model can utilize the strengths of both methods - the ability of ARIMA to handle the trend and seasonality, and the ability of RNNs to capture long-term dependencies and nonlinear relationships.

```python
import keras
from keras.models import Sequential
from keras.layers import LSTM, Dense
import statsmodels.api as sm

# Fit ARIMA model
arima_model = sm.tsa.ARIMA(data, order=(p, d, q)).fit()

# Get the residuals
residuals = arima_model.resid

# Train LSTM model on the residuals
model = Sequential()
model.add(LSTM(32, input_shape=(timesteps, features)))
model.add(Dense(1))

model.compile(loss='mean_squared_error', optimizer='adam')
model.fit(X, residuals, epochs=10, batch_size=32)

# Combine the forecasts from both models
combined_forecast = arima_model.predict(start, end) + model.predict(X_new)
```

## Conclusion

Hybrid models that combine ARIMA with other forecasting methods can be a powerful tool for improving the accuracy of time series forecasts. By leveraging the strengths of multiple models, the hybrid approach can handle complex patterns, nonlinear relationships, and outliers more effectively. However, it is important to carefully evaluate and tune these models based on the specific characteristics of the data to achieve the best results.

References:
- [Statsmodels documentation](https://www.statsmodels.org/stable/index.html)
- [Scikit-learn documentation](https://scikit-learn.org/stable/documentation.html)
- [Keras documentation](https://keras.io/)