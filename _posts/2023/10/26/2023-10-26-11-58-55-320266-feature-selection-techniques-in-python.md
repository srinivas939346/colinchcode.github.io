---
layout: post
title: "[python] Feature selection techniques in Python"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

Feature selection is an important step in machine learning and data analysis. It involves selecting a subset of relevant features from the dataset to improve the performance of the model and reduce overfitting. In this blog post, we will explore some popular feature selection techniques in Python.

## Table of Contents
- [Introduction](#introduction)
- [Filter Methods](#filter-methods)
  - [Variance Threshold](#variance-threshold)
  - [Chi-Square Test](#chi-square-test)
- [Wrapper Methods](#wrapper-methods)
  - [Recursive Feature Elimination](#recursive-feature-elimination)
  - [Forward Selection](#forward-selection)
- [Embedded Methods](#embedded-methods)
  - [Lasso Regression](#lasso-regression)
  - [Random Forest](#random-forest)
- [Conclusion](#conclusion)
- [References](#references)

## Introduction

Feature selection can be broadly categorized into three types: filter methods, wrapper methods, and embedded methods. Let's discuss each of them in detail.

## Filter Methods

Filter methods evaluate the relevance of features by examining their intrinsic properties without involving any machine learning algorithm.

### Variance Threshold

The variance threshold method removes features with low variance. It assumes that the features with low variance do not contain much information and are less likely to contribute to the model's performance. In Python, you can use the `VarianceThreshold` class from the scikit-learn library to implement this method.

```python
from sklearn.feature_selection import VarianceThreshold

def variance_threshold_selector(data, threshold):
    selector = VarianceThreshold(threshold)
    selector.fit(data)
    selected_features = data.columns[selector.get_support(indices=True)]
    return selected_features
```

### Chi-Square Test

The chi-square test measures the dependency between a categorical target variable and a categorical feature. It evaluates the significance of the relationship and selects the features with the highest chi-square statistics as relevant features. The `chi2` function from scikit-learn can be used to implement this method.

```python
from sklearn.feature_selection import SelectKBest, chi2

def chi_square_selector(data, target, k):
    selector = SelectKBest(chi2, k=k)
    selector.fit(data, target)
    selected_features = data.columns[selector.get_support(indices=True)]
    return selected_features
```

## Wrapper Methods

Wrapper methods involve training a machine learning model with different subsets of features and evaluating their performance.

### Recursive Feature Elimination

Recursive Feature Elimination (RFE) recursively eliminates features by training the model on the remaining features and selecting the least important one. It repeats this process until a desired number of features are left. The `RFE` class from scikit-learn can be used for this purpose.

```python
from sklearn.feature_selection import RFE
from sklearn.linear_model import LinearRegression

def recursive_feature_elimination(data, target, n_features):
    estimator = LinearRegression()
    selector = RFE(estimator, n_features_to_select=n_features)
    selector.fit(data, target)
    selected_features = data.columns[selector.support_]
    return selected_features
```

### Forward Selection

Forward selection starts with an empty feature set and iteratively adds the most relevant feature at each step. It evaluates the performance of the model with each added feature and stops when reaching the desired number of features or no further improvement is achieved. Forward selection can be implemented using a custom function in Python.

```python
from sklearn.linear_model import LinearRegression

def forward_selection(data, target, n_features):
    remaining_features = list(data.columns)
    selected_features = []
    num_features = min(n_features, len(remaining_features))

    while len(selected_features) < num_features:
        best_feature = None
        best_score = -1
        for feature in remaining_features:
            model = LinearRegression()
            features = selected_features + [feature]
            score = cross_val_score(model, data[features], target, cv=5).mean()
            if score > best_score:
                best_score = score
                best_feature = feature
        remaining_features.remove(best_feature)
        selected_features.append(best_feature)

    return selected_features
```

## Embedded Methods

Embedded methods combine the feature selection process with the model training process. They determine the feature importance during model training and select the relevant features accordingly.

### Lasso Regression

Lasso regression applies a penalty on the absolute value of the coefficients, forcing some of them to become zero. The features with non-zero coefficients are considered most relevant. The `Lasso` class from scikit-learn can be used to perform lasso regression.

```python
from sklearn.linear_model import Lasso

def lasso_regression_selector(data, target, alpha):
    selector = Lasso(alpha=alpha)
    selector.fit(data, target)
    selected_features = data.columns[selector.coef_ != 0]
    return selected_features
```

### Random Forest

Random Forest is an ensemble learning algorithm that creates multiple decision trees and combines their predictions. It calculates the feature importance based on how much each feature contributes to improving the purity of the decision trees. The `feature_importances_` attribute of the random forest model can be used to select the most important features.

```python
from sklearn.ensemble import RandomForestRegressor

def random_forest_selector(data, target, n_features):
    model = RandomForestRegressor()
    model.fit(data, target)
    feature_importances = model.feature_importances_
    indices = np.argsort(feature_importances)[::-1]
    selected_features = data.columns[indices[:n_features]]
    return selected_features
```

## Conclusion

Feature selection is a crucial step in machine learning model development. In this blog post, we discussed various feature selection techniques in Python, including filter methods, wrapper methods, and embedded methods. These techniques can help improve the model's performance and reduce overfitting by selecting the most relevant features from the dataset.

## References

- [scikit-learn documentation](https://scikit-learn.org/stable/)
- [Feature selection in machine learning - A complete guide](https://www.analyticsvidhya.com/blog/2020/10/feature-selection-techniques-in-machine-learning-an-ultimate-guide-with-examples/)
- [Feature selection techniques with Python](https://towardsdatascience.com/feature-selection-techniques-in-machine-learning-with-python-f24e7da3f36e)