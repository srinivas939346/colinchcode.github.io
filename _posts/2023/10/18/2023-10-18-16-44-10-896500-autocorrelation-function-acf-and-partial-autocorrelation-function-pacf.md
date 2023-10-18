---
layout: post
title: "[python] AutoCorrelation Function (ACF) and Partial AutoCorrelation Function (PACF)"
description: " "
date: 2023-10-18
tags: [python]
comments: true
share: true
---

In time series analysis, understanding the patterns and relationships in the data is crucial. Two commonly used tools for this purpose are the AutoCorrelation Function (ACF) and the Partial AutoCorrelation Function (PACF). These functions help us analyze the dependence between observations in a time series.

# AutoCorrelation Function (ACF)

The AutoCorrelation Function (ACF) measures the correlation between an observation and its lagged values at different time intervals. It provides information about the overall correlation structure of the time series.

The ACF plot is a bar chart that shows the correlation coefficients between each lagged value and the current observation. It is useful in identifying the presence of seasonality or trend in the data.

To calculate the ACF in Python, we can use the `acf` function from the `statsmodels` library. Here's an example:

```python
import statsmodels.api as sm

# Calculate ACF
acf_values = sm.tsa.stattools.acf(data, nlags=10)

# Plot ACF
sm.graphics.tsa.plot_acf(data, lags=10)
```

In this example, `data` is the time series data, and `nlags` specifies the number of lags to include in the ACF calculation. The `acf` function returns an array of ACF values, while the `plot_acf` function generates an ACF plot.

# Partial AutoCorrelation Function (PACF)

The Partial AutoCorrelation Function (PACF) measures the direct correlation between an observation and its lagged values, while accounting for the indirect correlation through intermediate lags. It provides information about the direct relationship between observations at different time intervals.

The PACF plot is a bar chart that shows the partial correlation coefficients between each lagged value and the current observation after accounting for the intermediate lags. It helps in identifying the order of an autoregressive (AR) model.

To calculate the PACF in Python, we can use the `pacf` function from the `statsmodels` library. Here's an example:

```python
import statsmodels.api as sm

# Calculate PACF
pacf_values = sm.tsa.stattools.pacf(data, nlags=10)

# Plot PACF
sm.graphics.tsa.plot_pacf(data, lags=10)
```

Similar to the ACF example, `data` refers to the time series data, and `nlags` specifies the number of lags to include in the PACF calculation. The `pacf` function returns an array of PACF values, while the `plot_pacf` function generates a PACF plot.

# Conclusion

The AutoCorrelation Function (ACF) and Partial AutoCorrelation Function (PACF) are valuable tools in analyzing the dependence and relationships within a time series. By calculating and visualizing the ACF and PACF, we can gain insights into the underlying patterns and determine the appropriate models for forecasting or further analysis.

References:
- [Statsmodels documentation](https://www.statsmodels.org/stable/tsa.html)
- [Wikipedia - Autocorrelation](https://en.wikipedia.org/wiki/Autocorrelation)
- [Wikipedia - Partial Autocorrelation](https://en.wikipedia.org/wiki/Partial_autocorrelation_function)