---
layout: post
title: "[python] Rolling forecasts with ARIMA models"
description: " "
date: 2023-10-18
tags: [python]
comments: true
share: true
---

In time series forecasting, it is often useful to perform rolling forecasts, where the model is updated recursively as new data becomes available. This approach allows us to evaluate the performance of the model in real-time and make more accurate predictions.

In this blog post, we will discuss how to implement rolling forecasts using ARIMA models in Python.

## What is an ARIMA model?

ARIMA stands for autoregressive integrated moving average. It is a popular model for time series forecasting that takes into account the autoregressive, integrated, and moving average components of the data.

The autoregressive (AR) component refers to the dependency of the current value on previous values. The integrated (I) component refers to the differencing applied to make the time series stationary. The moving average (MA) component refers to the dependency of the current value on the past forecast errors.

## Rolling forecasting with ARIMA models

To perform rolling forecasts with ARIMA models, we follow these steps:

1. Split the time series data into a training set and a test set. The training set contains the historical data used to train the model, while the test set contains the data used to evaluate the model's performance.

2. Initialize the ARIMA model with the training data.

3. Iterate over the test set in a rolling manner, one step at a time.

4. For each step, fit the ARIMA model to the training data up to the current step.

5. Make a one-step ahead forecast using the fitted model.

6. Update the training data by appending the current step from the test set.

7. Evaluate the performance of the forecast by comparing it to the actual value from the test set.

8. Repeat steps 4 to 7 until all steps in the test set are covered.

Let's see an example implementation using the `statsmodels` library in Python:

```python
import pandas as pd
from statsmodels.tsa.arima.model import ARIMA

# Load the time series data
data = pd.read_csv('data.csv')

# Split the data into training and test sets
train_data = data[:80]
test_data = data[80:]

# Initialize the ARIMA model
model = ARIMA(train_data, order=(2, 1, 1))

# Iterate over the test set
predictions = []
for i in range(len(test_data)):
    # Fit the model to the training data
    model_fit = model.fit()

    # Make a one-step ahead forecast
    forecast = model_fit.forecast(steps=1)

    # Append the forecast to the predictions list
    predictions.append(forecast[0])

    # Update the training data
    train_data = train_data.append(test_data.iloc[i])

# Evaluate the performance of the forecast
mse = ((test_data['value'] - predictions) ** 2).mean()
```

In this example, we load the time series data and split it into a training set (first 80 data points) and a test set (remaining data points). We then initialize the ARIMA model with an order of (2, 1, 1), indicating two autoregressive terms, one differencing term, and one moving average term.

We iterate over the test set and fit the model to the training data up to the current step. We make a one-step ahead forecast using the fitted model and append it to the predictions list. We also update the training data by appending the current step from the test set.

Finally, we evaluate the performance of the forecast by calculating the mean squared error (MSE) between the predicted values and the actual values from the test set.

## Conclusion

In this blog post, we discussed how to perform rolling forecasts with ARIMA models in Python. Rolling forecasts are useful for evaluating the performance of time series models and making accurate predictions in real-time. By following the steps outlined above, you can implement rolling forecasts with ARIMA models in your own time series forecasting projects.

References:
- [StatsModels Documentation](https://www.statsmodels.org/stable/index.html)