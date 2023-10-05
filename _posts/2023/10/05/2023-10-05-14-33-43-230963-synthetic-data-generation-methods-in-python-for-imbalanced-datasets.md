---
layout: post
title: "[python] Synthetic data generation methods in Python for imbalanced datasets"
description: " "
date: 2023-10-05
tags: [python]
comments: true
share: true
---

In many real-world machine learning applications, we encounter imbalanced datasets where the number of instances belonging to one class is significantly higher or lower than the other classes. Imbalanced datasets pose a challenge for building accurate models as they tend to bias the predictions towards the majority class.

One way to handle imbalanced datasets is by using synthetic data generation methods. Synthetic data generation involves creating artificial data points for minority or under-represented classes to balance the dataset. In this article, we will explore some popular synthetic data generation methods implemented in Python.

## Table of Contents
- [Introduction](#introduction)
- [1. Synthetic Minority Over-sampling Technique (SMOTE)](#smote)
- [2. Adaptive Synthetic Sampling (ADASYN)](#adasyn)
- [3. Synthetic Data Augmentation (SDA)](#sda)
- [Conclusion](#conclusion)

## Introduction<a name="introduction"></a>
Synthetic data generation methods can help address imbalanced datasets by creating artificially generated data points for the minority classes. These methods aim to balance the distribution of instances across different classes and improve the performance of classification models.

In this article, we will cover three popular synthetic data generation methods implemented in Python: SMOTE, ADASYN, and SDA.

## 1. Synthetic Minority Over-sampling Technique (SMOTE)<a name="smote"></a>
SMOTE is a widely used synthetic data generation algorithm for imbalanced datasets. It works by interpolating new synthetic instances between the existing instances of the minority class.

The SMOTE algorithm follows these steps:
1. Randomly select a minority class instance.
2. Find its k nearest neighbors from the minority class instances.
3. Randomly select one neighbor, and generate a synthetic instance between the selected instance and its neighbor.
4. Repeat steps 1-3 until the desired number of synthetic instances is generated.

Here is an example code snippet to demonstrate how to use the `imbalanced-learn` library in Python to perform SMOTE:

```python
from imblearn.over_sampling import SMOTE

# Instantiate SMOTE
smote = SMOTE()

# Generate synthetic data using SMOTE
X_resampled, y_resampled = smote.fit_resample(X, y)
```

## 2. Adaptive Synthetic Sampling (ADASYN)<a name="adasyn"></a>
ADASYN is an extension of SMOTE that focuses on generating synthetic data points for the minority class instances that are harder to learn. It dynamically adjusts the distribution of synthetic samples based on the density of different minority class regions.

The ADASYN algorithm follows these steps:
1. Randomly select a minority class instance.
2. Calculate the density ratio of each minority class instance's k nearest neighbors.
3. Normalize the density ratios to determine the relevance of different instances.
4. Generate synthetic instances near the hardest to learn minority instances.
5. Repeat steps 1-4 until the desired class balance is achieved.

Here is an example code snippet to demonstrate how to use the `imbalanced-learn` library in Python to perform ADASYN:

```python
from imblearn.over_sampling import ADASYN

# Instantiate ADASYN
adasyn = ADASYN()

# Generate synthetic data using ADASYN
X_resampled, y_resampled = adasyn.fit_resample(X, y)
```

## 3. Synthetic Data Augmentation (SDA)<a name="sda"></a>
SDA is another popular technique for generating synthetic data to handle imbalanced datasets. It works by applying data augmentation techniques such as rotation, translation, or flipping to the existing minority class instances to create new synthetic samples.

The SDA algorithm follows these steps:
1. Randomly select a minority class instance.
2. Apply data augmentation techniques (e.g., rotation, translation) to the selected instance to create a new synthetic instance.
3. Repeat steps 1-2 until the desired number of synthetic instances is generated.

Here is an example code snippet to demonstrate how to use the `albumentations` library in Python to perform SDA:

```python
import albumentations as A

# Define data augmentation transforms
transforms = A.Compose([
    A.Rotate(),
    A.HorizontalFlip(),
    A.VerticalFlip()
])

# Apply data augmentation to minority class instances
augmented_images = []
for img in minority_class_images:
    augmented = transforms(image=img)
    augmented_images.append(augmented['image'])
```

## Conclusion<a name="conclusion"></a>
Synthetic data generation methods such as SMOTE, ADASYN, and SDA provide powerful techniques to address imbalanced datasets. These methods can help balance the class distribution by generating synthetic data points for under-represented classes, thus improving the performance of machine learning models.

By using Python libraries like `imbalanced-learn` and `albumentations`, you can easily implement these synthetic data generation methods and apply them to your imbalanced datasets. Remember to experiment with different methods and evaluate their impact on model performance to find the most suitable approach.