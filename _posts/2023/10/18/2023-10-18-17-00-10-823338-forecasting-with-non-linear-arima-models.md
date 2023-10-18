---
layout: post
title: "[python] Forecasting with non-linear ARIMA models"
description: " "
date: 2023-10-18
tags: [python]
comments: true
share: true
---

In time series analysis, Autoregressive Integrated Moving Average (ARIMA) models are commonly used for modeling and forecasting stationary time series data. However, there are cases where the underlying dynamics of the time series may not be adequately captured by a linear ARIMA model.

In such situations, we can employ non-linear ARIMA models, also known as non-linear autoregressive moving average (NARMA) models, which can capture non-linear relationships in the data. This can be particularly useful for forecasting in domains with complex and nonlinear dynamics, such as financial markets or weather prediction.

## Non-linear ARIMA models

Non-linear ARIMA models extend the traditional linear ARIMA models by introducing non-linear terms to capture the potentially non-linear relationships in the data. While the structure of a non-linear ARIMA model may vary, a common approach is to use polynomial terms or lagged values of the series as input variables.

## Implementing non-linear ARIMA models in Python

In Python, we can use the `statsmodels` library to implement non-linear ARIMA models. Here's an example code snippet demonstrating how to fit a non-linear ARIMA model and make forecasts:

```python
import statsmodels.api as sm
import numpy as np

# Assuming 'data' is the time series data to be forecasted
# lag1 and lag2 are lagged values of the series
# coef1 and coef2 are coefficients for the non-linear terms

# Create the design matrix
X = np.column_stack((data, lag1, lag2, coef1*data**2, coef2*data**3))

# Fit the non-linear ARIMA model
model = sm.OLS(data, X)
results = model.fit()

# Make forecasts
forecast_horizon = 10
forecast = results.predict(X[-forecast_horizon:])
```

In this example, we first create a design matrix `X` by stacking the original time series values (`data`), the lagged values (`lag1` and `lag2`), and the non-linear terms (`coef1*data**2` and `coef2*data**3`). We then fit an ordinary least squares (OLS) regression model using `sm.OLS` and make forecasts using `results.predict` method.

## Conclusion

Non-linear ARIMA models offer a flexible approach for capturing non-linear relationships in time series data. They can be useful in situations where linear models fail to capture the underlying dynamics adequately. With the help of the `statsmodels` library in Python, implementing and forecasting with non-linear ARIMA models becomes straightforward.

References:
- [Statsmodels documentation](https://www.statsmodels.org/stable/index.html)
- Makridakis, S., Hyndman, R.J., & Nikolopoulos, K. (2020). Forecasting: Methods and Applications. Wiley.