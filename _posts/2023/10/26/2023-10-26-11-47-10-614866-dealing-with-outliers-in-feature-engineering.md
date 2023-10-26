---
layout: post
title: "[python] Dealing with outliers in feature engineering"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

Outliers, or extreme values in a dataset, can have a significant impact on the quality and effectiveness of machine learning models. They can skew the distribution of the data, affect the calculation of summary statistics, and introduce noise or misleading patterns.

In this blog post, we will explore different techniques for dealing with outliers in feature engineering using Python.

## Table of Contents
1. [What are Outliers?](#what-are-outliers)
2. [Identifying Outliers](#identifying-outliers)
3. [Handling Outliers](#handling-outliers)
    - [1. Removing Outliers](#removing-outliers)
    - [2. Transforming Features](#transforming-features)
    - [3. Discretization](#discretization)
    - [4. Robust Statistics](#robust-statistics)
4. [Conclusion](#conclusion)

## What are Outliers?
Outliers are data points that significantly differ from the majority of the observations in a dataset. They can be caused by errors in data collection, measurement errors, or genuinely unusual observations. 

## Identifying Outliers
Before dealing with outliers, it's essential to identify them first. There are several methods for identifying outliers, such as:

1. **Statistical Methods**: Using summary statistics like mean, standard deviation, and Z-scores, outliers can be detected by looking for values that fall outside a given threshold.

2. **Visualization Techniques**: Plotting the data can help identify outliers visually. Box plots, scatter plots, and histograms can provide insights into the distribution of the data and reveal potential outliers.

## Handling Outliers

Once outliers have been identified, there are several approaches to handle them:

### 1. Removing Outliers
The simplest approach is to remove the outliers from the dataset. This can be done by either deleting the entire row containing an outlier or imputing missing values in place of outliers. However, caution should be exercised as this approach may lead to a loss of information or bias the remaining data.

```python
import numpy as np

# Remove outliers using a specified threshold
def remove_outliers(data, threshold):
    mean = np.mean(data)
    std = np.std(data)
    return [x for x in data if (mean - 2 * std < x < mean + 2 * std)]
```

### 2. Transforming Features
Another approach is to transform the feature containing outliers. This can be achieved by using mathematical functions such as logarithm, square root, or power transformation. These transformations can help normalize the data and reduce the impact of outliers.

```python
import numpy as np

# Apply log transformation to a feature
def log_transform(data):
    return np.log(data)
```

### 3. Discretization
Discretization involves converting continuous variables into discrete categories. By dividing the range of values into bins, outliers can be assigned to a specific range, thus reducing their impact.

```python
import pandas as pd

# Discretize a feature into bins
def discretize_feature(data, bins):
    return pd.cut(data, bins=bins)
```

### 4. Robust Statistics
Robust statistics methods are designed to be less influenced by outliers. For example, using the median instead of the mean can provide a more robust measure of central tendency.

```python
import numpy as np

# Calculate median absolute deviation (MAD)
def calculate_mad(data):
    median = np.median(data)
    absolute_deviations = np.abs(data - median)
    return np.median(absolute_deviations)
```

## Conclusion
Outliers can have a significant impact on the performance of machine learning models. Therefore, it is crucial to identify and handle them appropriately during feature engineering. This blog post discussed various approaches for dealing with outliers, including removal, transformation, discretization, and robust statistics. The choice of approach depends on the specific dataset and the goals of the analysis.

Remember, always analyze and understand the context of your data before adopting any outlier handling techniques.

References:
- [Wikipedia - Outlier](https://en.wikipedia.org/wiki/Outlier)
- [Towards Data Science - Dealing with Outliers](https://towardsdatascience.com/dealing-with-outliers-in-machine-learning-1bbe04e3a834)