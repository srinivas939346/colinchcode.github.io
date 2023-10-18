---
layout: post
title: "[python] Estimating model parameters in ARIMA"
description: " "
date: 2023-10-18
tags: [python]
comments: true
share: true
---

In time series analysis, ARIMA (AutoRegressive Integrated Moving Average) is a popular model used to forecast data points based on their historical values. One of the key steps in using ARIMA is estimating the model parameters.

The parameters in an ARIMA model are denoted by `(p, d, q)`, where:
- `p` represents the order of the AutoRegressive (AR) component
- `d` represents the degree of differencing required to make the time series stationary
- `q` represents the order of the Moving Average (MA) component

In this blog post, we will focus on estimating these parameters using the [Python](https://www.python.org/) programming language and the [statsmodels](https://www.statsmodels.org/stable/index.html) library.

## Dataset

Before diving into estimating ARIMA parameters, let's start by loading a sample dataset that we will use for demonstration purposes. We will use the AirPassengers dataset, which contains the monthly number of airline passengers from 1949 to 1960.

```python
import pandas as pd

# Load the dataset
df = pd.read_csv('AirPassengers.csv')
df.head()
```

## Differencing

The first step in estimating ARIMA parameters is to make the time series stationary through differencing. A stationary time series has a constant mean, variance, and autocovariance and is a prerequisite for ARIMA modeling.

To determine the degree of differencing `(d)`, we can plot the autocorrelation function (ACF) and partial autocorrelation function (PACF) of the time series. The ACF shows the correlation between a time series and its lagged values, while the PACF shows the correlation between a time series and its lagged values, excluding the effects of intervening lags.

```python
import matplotlib.pyplot as plt
from statsmodels.graphics.tsaplots import plot_acf, plot_pacf

# Plot ACF and PACF
fig, axes = plt.subplots(1, 2, figsize=(12, 4))
plot_acf(df['Passengers'], ax=axes[0])
plot_pacf(df['Passengers'], ax=axes[1])
plt.show()
```

## Autoregressive (AR) Component - `p`

The autoregressive (AR) component represents the dependency between the current observation and a number of lagged observations. To estimate the order of the AR component `(p)`, we can examine the PACF plot and observe where the partial autocorrelation values drop off significantly.

```python
from statsmodels.tsa.ar_model import AR

# Fit AR model
model_ar = AR(df['Passengers'])
model_ar_fit = model_ar.fit()

# Print the order of the AR component
p = model_ar_fit.k_ar
print(f"The order of the AR component (p) is {p}")
```

## Moving Average (MA) Component - `q`

The moving average (MA) component represents the dependency between the current observation and a number of lagged errors. To estimate the order of the MA component `(q)`, we can examine the ACF plot and observe where the autocorrelation values drop off significantly.

```python
from statsmodels.tsa.arima_model import ARMA

# Fit MA model
model_ma = ARMA(df['Passengers'], order=(0, 1))
model_ma_fit = model_ma.fit(disp=False)

# Print the order of the MA component
q = model_ma_fit.k_ma
print(f"The order of the MA component (q) is {q}")
```

## Conclusion

Estimating the model parameters in ARIMA is a crucial step in time series analysis. By understanding the orders of the autoregressive (AR) and moving average (MA) components, we can build an accurate ARIMA model for forecasting. Python and the statsmodels library provide powerful tools to estimate these parameters and perform advanced time series analysis.

Remember to always validate and fine-tune the ARIMA model using techniques like model diagnostics and evaluation metrics.

Keep exploring and experimenting with different datasets and model configurations to improve your forecasting skills!