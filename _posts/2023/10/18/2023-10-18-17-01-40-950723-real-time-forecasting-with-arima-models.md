---
layout: post
title: "[python] Real-time forecasting with ARIMA models"
description: " "
date: 2023-10-18
tags: [python]
comments: true
share: true
---

In the field of time series analysis, ARIMA (AutoRegressive Integrated Moving Average) models are widely used for forecasting future values based on historical data. One of the key advantages of ARIMA models is their ability to handle non-stationary time series data by applying differencing operations.

In this article, we will explore how to implement real-time forecasting using ARIMA models in Python. We will start by installing the necessary libraries and then proceed with an example.

## Table of Contents
- [Installing required libraries](#installing-required-libraries)
- [Implementing real-time forecasting](#implementing-real-time-forecasting)
- [Example](#example)

## Installing required libraries

To get started, we need to install the `pandas`, `numpy`, and `statsmodels` libraries. You can install these libraries using pip:

```python
pip install pandas numpy statsmodels
```

## Implementing real-time forecasting

To implement real-time forecasting with ARIMA models, we need historical time series data and the latest observation. The process involves fitting an ARIMA model to the historical data and using it to forecast the future values.

Here's a step-by-step guide for implementing real-time forecasting:

1. Import the required libraries:

```python
import pandas as pd
import numpy as np
from statsmodels.tsa.arima.model import ARIMA
```

2. Load the historical time series data:

```python
historical_data = pd.read_csv('historical_data.csv')
```

3. Fit an ARIMA model to the historical data:

```python
model = ARIMA(historical_data, order=(p, d, q))
model.fit()
```

4. Obtain the latest observation:

```python
latest_observation = historical_data.iloc[-1]
```

5. Forecast future values using the ARIMA model:

```python
forecast = model.forecast(steps=10)  # forecasting 10 steps ahead
```

6. Combine the latest observation and the forecasted values:

```python
real_time_forecast = pd.concat([latest_observation, forecast])
```

7. Display the real-time forecast:

```python
print(real_time_forecast)
```

## Example

Let's demonstrate real-time forecasting with a simple example. Consider the following historical time series data:

```
Timestamp,Value
2021-01-01,10
2021-01-02,15
2021-01-03,20
2021-01-04,25
2021-01-05,30
```

Using the steps discussed above, we can implement real-time forecasting:

```python
import pandas as pd
import numpy as np
from statsmodels.tsa.arima.model import ARIMA

historical_data = pd.read_csv('historical_data.csv')

model = ARIMA(historical_data['Value'], order=(1, 1, 1))
model.fit()

latest_observation = historical_data['Value'].iloc[-1]

forecast = model.forecast(steps=3)  # forecasting 3 steps ahead

real_time_forecast = pd.concat([latest_observation, forecast])

print(real_time_forecast)
```

Running this example will print the real-time forecast for the next 3 steps based on the historical data.

Now you have a basic understanding of how to implement real-time forecasting with ARIMA models in Python. With the help of these models, you can make accurate predictions based on the latest available data. Experiment with different ARIMA parameters and explore more advanced techniques to enhance your forecasting capabilities.

## References

- [statsmodels documentation](https://www.statsmodels.org/stable/generated/statsmodels.tsa.arima.model.ARIMA.html)
- [ARIMA model on Wikipedia](https://en.wikipedia.org/wiki/Autoregressive_integrated_moving_average)