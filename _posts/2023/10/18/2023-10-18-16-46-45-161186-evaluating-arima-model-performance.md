---
layout: post
title: "[python] Evaluating ARIMA model performance"
description: " "
date: 2023-10-18
tags: [python]
comments: true
share: true
---

ARIMA (AutoRegressive Integrated Moving Average) models are widely used in time series forecasting. Once we have built an ARIMA model, it is important to evaluate its performance to ensure its effectiveness in predicting future values. In this blog post, we will discuss some commonly used evaluation techniques for ARIMA models.

## Table of Contents
1. [Mean Absolute Error (MAE)](#mean-absolute-error-mae)
2. [Root Mean Square Error (RMSE)](#root-mean-square-error-rmse)
3. [Mean Absolute Percentage Error (MAPE)](#mean-absolute-percentage-error-mape)
4. [Ljung-Box Test for Residuals](#ljung-box-test-for-residuals)
5. [Akaike Information Criterion (AIC)](#akaike-information-criterion-aic)
6. [Bayesian Information Criterion (BIC)](#bayesian-information-criterion-bic)

## Mean Absolute Error (MAE)
The Mean Absolute Error (MAE) measures the average magnitude of errors in predictions. It is calculated by taking the absolute difference between actual and predicted values and then averaging them.

```python
import numpy as np

def calculate_mae(actual, predicted):
    return np.mean(np.abs(actual - predicted))
```

## Root Mean Square Error (RMSE)
The Root Mean Square Error (RMSE) is another commonly used metric to evaluate model performance. It represents the square root of the average of squared differences between actual and predicted values.

```python
def calculate_rmse(actual, predicted):
    return np.sqrt(np.mean((actual - predicted)**2))
```

## Mean Absolute Percentage Error (MAPE)
The Mean Absolute Percentage Error (MAPE) measures the average percentage deviation of actual values from predicted values. It is useful when comparing the performance of models with different scales.

```python
def calculate_mape(actual, predicted):
    return np.mean(np.abs((actual - predicted) / actual)) * 100
```

## Ljung-Box Test for Residuals
The Ljung-Box test is a statistical test used to check for the presence of autocorrelation in the residuals of an ARIMA model. It helps determine if the model captures all the information in the data and if there is still information left unexplained.

## Akaike Information Criterion (AIC)
The Akaike Information Criterion (AIC) is a measure of the quality of a statistical model. It takes into account both the goodness of fit and the complexity of the model. AIC penalizes models with larger number of parameters, thereby preventing overfitting.

## Bayesian Information Criterion (BIC)
The Bayesian Information Criterion (BIC) is similar to AIC but places a higher penalty on models with more parameters. It provides a balance between model complexity and goodness of fit, allowing for a more precise model selection.

These are just a few of the evaluation techniques used for ARIMA model performance. It is important to choose the most appropriate metrics based on the specific requirements and characteristics of your data. By evaluating the performance of your ARIMA model, you can make informed decisions and fine-tune your forecasting process.