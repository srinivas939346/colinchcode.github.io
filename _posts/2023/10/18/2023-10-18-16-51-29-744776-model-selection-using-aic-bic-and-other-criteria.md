---
layout: post
title: "[python] Model selection using AIC, BIC, and other criteria"
description: " "
date: 2023-10-18
tags: [python]
comments: true
share: true
---

When building statistical models, it is essential to choose the most appropriate model that adequately captures the relationship between variables and explains the underlying phenomena. Model selection is a critical step in the modeling process as it helps avoid overfitting or underfitting the data. In this blog post, we will explore two widely used model selection criteria: AIC (Akaike Information Criterion) and BIC (Bayesian Information Criterion), along with other commonly used criteria.

## What is AIC?

AIC, developed by Hirotsugu Akaike, is a measurement of the quality of a statistical model. It provides a balance between the model's goodness of fit to the data and its complexity in terms of the number of parameters. The AIC value is calculated using the formula: 

```
AIC = -2log(L) + 2k
```

Where `L` is the maximized value of the likelihood function of the model, and `k` is the number of parameters in the model.

## What is BIC?

Similar to AIC, the Bayesian Information Criterion (BIC) also measures the quality of a statistical model. However, BIC has a more stringent penalty for model complexity. The BIC value is calculated using the following formula:

```
BIC = -2log(L) + klog(n)
```

Where `L` is the maximized value of the likelihood function, `k` is the number of parameters, and `n` is the sample size.

## AIC vs. BIC

Both AIC and BIC can be used for model selection. The main difference lies in the penalty term for model complexity. AIC applies a less stringent penalty, making it more suitable when sample size is small, while BIC applies a stronger penalty, favoring simpler models.

## Other Model Selection Criteria

Apart from AIC and BIC, there are other commonly used model selection criteria:

- **Adjusted R-squared**: This criterion penalizes the addition of unnecessary predictors by adjusting the R-squared value based on the number of predictors in the model.
- **Mallow's Cp**: Cp statistic compares the fitted model's predictive accuracy with that of the full model.
- **Cross-validation**: This technique estimates the model's performance by splitting the data into training and validation sets. It measures the model's ability to generalize to new data.

## Conclusion

Model selection is a crucial step in the modeling process, and AIC, BIC, and other criteria help find the most appropriate model for the given data. AIC and BIC strike a balance between model fit and complexity, while other criteria such as adjusted R-squared, Mallow's Cp, and cross-validation provide additional insights into model performance. By considering these criteria, researchers and data scientists can make informed decisions while building statistical models.

> References:
> 
> [1] Akaike, H. (1974). A new look at the statistical model identification. *IEEE transactions on automatic control, 19(6)*, 716-723.
> 
> [2] Schwartz, G. (1978). Estimating the dimension of a model. *The annals of statistics, 6(2)*, 461-464.