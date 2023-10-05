---
layout: post
title: "[python] Undersampling techniques in Python for imbalanced datasets"
description: " "
date: 2023-10-05
tags: [python]
comments: true
share: true
---

Dealing with imbalanced datasets is a common challenge in machine learning. When the classes in the dataset are not represented equally, it can lead to biased models that favor the majority class. One approach to address this issue is undersampling, which involves reducing the number of instances from the majority class.

In this article, we will explore some popular undersampling techniques implemented in Python that can be used to tackle imbalanced datasets.

## Table of Contents
1. [What is Undersampling?](#what-is-undersampling)
2. [Random Undersampling](#random-undersampling)
3. [NearMiss Undersampling](#nearmiss-undersampling)
4. [Instance Hardness Threshold (IHT) Undersampling](#instance-hardness-threshold-iht-undersampling)
5. [Conclusion](#conclusion)

## What is Undersampling? 

Undersampling is a technique used to balance imbalanced datasets by reducing the number of instances from the majority class. This approach lowers the dominance of the majority class and increases the presence of the minority class, leading to a more balanced training dataset.

## Random Undersampling

Random undersampling is the simplest form of undersampling, where random instances from the majority class are removed to balance the dataset. It is often used when the dataset has a large number of instances, and it allows for a faster training process.

The following Python code demonstrates random undersampling using the `imbalanced-learn` library:

```python
from imblearn.under_sampling import RandomUnderSampler

# Instantiate the random undersampler
undersampler = RandomUnderSampler(random_state=42)

# Perform undersampling on the dataset
X_res, y_res = undersampler.fit_resample(X, y)
```

## NearMiss Undersampling

NearMiss is an undersampling technique that selects instances from the majority class based on their distance to instances in the minority class. There are several variations of NearMiss available, such as NearMiss-1, NearMiss-2, and NearMiss-3.

Using the `imbalanced-learn` library, you can implement NearMiss undersampling as follows:

```python
from imblearn.under_sampling import NearMiss

# Instantiate the NearMiss undersampler
undersampler = NearMiss(version=1)

# Perform undersampling on the dataset
X_res, y_res = undersampler.fit_resample(X, y)
```

## Instance Hardness Threshold (IHT) Undersampling

Instance Hardness Threshold (IHT) undersampling selects instances from the majority class based on the hardness scores computed by a classifier. It focuses on the instances that are closest to the decision boundary, as they are often the most difficult to classify correctly.

Here's an example of implementing IHT undersampling using the `imbalanced-learn` library:

```python
from imblearn.under_sampling import InstanceHardnessThreshold
from sklearn.ensemble import RandomForestClassifier

# Instantiate the classifier for computing hardness scores
clf = RandomForestClassifier(random_state=42)

# Instantiate the IHT undersampler
undersampler = InstanceHardnessThreshold(estimator=clf, sampling_strategy='auto')

# Perform undersampling on the dataset
X_res, y_res = undersampler.fit_resample(X, y)
```

## Conclusion

Undersampling can be an effective technique for dealing with imbalanced datasets in machine learning. In this article, we have explored some popular undersampling techniques implemented in Python, including random undersampling, NearMiss undersampling, and Instance Hardness Threshold (IHT) undersampling.

The choice of the undersampling technique depends on the characteristics of the dataset and the problem at hand. It is essential to experiment with different techniques to find the most suitable approach for improving the performance of machine learning models on imbalanced datasets.