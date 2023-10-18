---
layout: post
title: "[python] Implementing ARIMA models in Python using pmdarima"
description: " "
date: 2023-10-18
tags: [python]
comments: true
share: true
---

**Introduction**

ARIMA (AutoRegressive Integrated Moving Average) models are widely used in time series analysis and forecasting. They can be used to model and predict the future values of a time series based on its past values. In this blog post, we will explore how to implement ARIMA models in Python using the `pmdarima` library.

**Installing pmdarima**

Before we can start using `pmdarima`, we need to install it. To install `pmdarima`, you can use pip by running the following command:

```
pip install pmdarima
```

**Importing the necessary libraries**

After installing `pmdarima`, we need to import it along with some other necessary libraries to work with time series data. Here is an example of how to import the required libraries:

```python
import pandas as pd
import numpy as np
import pmdarima as pm
import matplotlib.pyplot as plt
```

**Loading the dataset**

Let's assume we have a time series dataset stored in a CSV file. We can load the dataset using the `pandas` library as follows:

```python
df = pd.read_csv('dataset.csv', parse_dates=['date_column'], index_col='date_column')
```

Make sure to replace `'dataset.csv'` with the actual path to your dataset file, and `'date_column'` with the name of the column that contains the date or time information.

**Exploratory Data Analysis**

Before fitting an ARIMA model, it's important to perform exploratory data analysis (EDA) to understand the properties of the time series. This includes visualizing the time series, checking for trends, seasonality, and stationarity.

```python
plt.plot(df)
plt.xlabel('Date')
plt.ylabel('Value')
plt.title('Time Series Plot')
plt.show()
```

**Training the ARIMA model**

To train an ARIMA model, we can use the `auto_arima` function provided by `pmdarima`. This function automatically selects the best parameters for the ARIMA model based on an information criterion.

```python
model = pm.auto_arima(df, start_p=1, start_q=1,
                      max_p=3, max_q=3, m=12,
                      start_P=0, seasonal=True,
                      d=None, D=1, trace=True,
                      error_action='ignore',  
                      suppress_warnings=True, 
                      stepwise=True)
```

Here, we specify the starting values for the AR, MA, and seasonal components, as well as the maximum values for these components. The `m` parameter represents the number of periods in each season (e.g., 12 for monthly data with annual seasonality). Setting `seasonal=True` enables the seasonal component.

**Forecasting**

Once the model is trained, we can use it to make predictions on future values. The `predict` function can be used to generate forecasts.

```python
forecast = model.predict(n_periods=10)
```

In this example, we generate forecasts for the next 10 periods. Adjust the `n_periods` parameter as needed for your specific use case.

**Model evaluation**

After making predictions, it's essential to evaluate the performance of the model. Common evaluation metrics for time series forecasting include mean absolute error (MAE), root mean squared error (RMSE), and mean absolute percentage error (MAPE).

```python
from sklearn.metrics import mean_absolute_error, mean_squared_error

actual_values = df.iloc[-10:].values  # Actual values for the last 10 periods

mae = mean_absolute_error(actual_values, forecast)
rmse = np.sqrt(mean_squared_error(actual_values, forecast))
mape = np.mean(np.abs((actual_values - forecast) / actual_values)) * 100

print('MAE:', mae)
print('RMSE:', rmse)
print('MAPE:', mape)
```

**Conclusion**

In this blog post, we learned how to implement ARIMA models in Python using the `pmdarima` library. We covered the steps of loading the dataset, performing exploratory data analysis, training the ARIMA model, making forecasts, and evaluating the model's performance. ARIMA models can be a valuable tool for time series analysis and forecasting in various domains.