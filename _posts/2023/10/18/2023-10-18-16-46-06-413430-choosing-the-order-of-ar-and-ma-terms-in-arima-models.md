---
layout: post
title: "[python] Choosing the order of AR and MA terms in ARIMA models"
description: " "
date: 2023-10-18
tags: [python]
comments: true
share: true
---

When building an ARIMA (Autoregressive Integrated Moving Average) model, one important step is to determine the order of the autoregressive (AR) and moving average (MA) terms. The order of these terms greatly influences the model's predictive power and performance.

## Understanding AR, MA, and ARIMA models

Before we dive into the selection of AR and MA terms, let's briefly understand what they represent in ARIMA models:

- **Autoregressive (AR) Term**: This term represents the dependence of the current value on past values. It assumes that the future value of a time series depends on its previous values. The order of the AR term determines how many past values to consider.

- **Moving Average (MA) Term**: This term represents the dependence of the current value on past error terms. It assumes that the current value depends on the error terms of previous predictions. The order of the MA term determines how many past error terms to consider.

- **ARIMA Model**: ARIMA models combine both the AR and MA terms, along with the integration term (I) that deals with non-stationary data. The order of the ARIMA model is denoted as (p, d, q), where p denotes the AR order, d denotes the differencing order, and q denotes the MA order.

## Selecting the Order of AR and MA Terms

Determining the order of AR and MA terms is often an iterative process. Here are a few methods and techniques to guide you:

### 1. Partial Autocorrelation Function (PACF)

The Partial Autocorrelation Function (PACF) helps identify the direct effect of one variable on another while controlling the effects of the intermediate variables. Plotting the PACF helps determine the order of the AR term. 

To plot the PACF in Python, you can use the `statsmodels` library:

```python
import statsmodels.api as sm
from statsmodels.graphics.tsaplots import plot_pacf

# Assuming your time series is stored in 'data'
plot_pacf(data)
```

The number of spikes that cross the significance level in the PACF plot indicates the order of the AR term.

### 2. Autocorrelation Function (ACF)

The Autocorrelation Function (ACF) measures the correlation between a time series and its lagged values. Plotting the ACF helps determine the order of the MA term.

To plot the ACF in Python, you can use the `statsmodels` library:

```python
import statsmodels.api as sm
from statsmodels.graphics.tsaplots import plot_acf

# Assuming your time series is stored in 'data'
plot_acf(data)
```

The number of spikes that cross the significance level in the ACF plot indicates the order of the MA term.

### 3. Information Criterion

An information criterion, such as the Akaike Information Criterion (AIC) or Bayesian Information Criterion (BIC), can be used to quantify the goodness of fit for different models with varying orders of AR and MA terms. The lower the AIC or BIC value, the better the model.

```python
import statsmodels.api as sm

# Assuming your time series is stored in 'data'
model = sm.tsa.ARIMA(data, order=(p, d, q))
results = model.fit()

print(results.aic)
print(results.bic)
```

Try fitting models with different values of p and q and choose the one with the lowest AIC or BIC.

## Conclusion

Choosing the right order of AR and MA terms is essential for building accurate ARIMA models. By analyzing the PACF, ACF, and using information criteria, you can gain insight into the appropriate order of the terms. Experimenting with different combinations and evaluating the chosen criteria will help you find the best configuration for your ARIMA model.

References:
- StatsModels Documentation: [https://www.statsmodels.org/stable/index.html](https://www.statsmodels.org/stable/index.html)