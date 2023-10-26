---
layout: post
title: "[python] Evaluating the impact of feature engineering on model performance"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---
Feature engineering is a crucial step in the machine learning pipeline that involves transforming raw data into a format that can be easily understood by a machine learning algorithm. By engineering new features or modifying existing ones, we aim to improve the performance of our models.

In this blog post, we will explore the impact of feature engineering on model performance using Python. We will walk through an example where we apply various feature engineering techniques and evaluate the effect they have on a classifier model.

## Table of Contents
- [Introduction](#introduction)
- [Data Preparation](#data-preparation)
- [Baseline Model](#baseline-model)
- [Feature Engineering Techniques](#feature-engineering-techniques)
  - [Scaling](#scaling)
  - [Encoding Categorical Variables](#encoding-categorical-variables)
  - [Creating Interaction Terms](#creating-interaction-terms)
  - [Handling Missing Values](#handling-missing-values)
- [Model Evaluation](#model-evaluation)
- [Conclusion](#conclusion)

## Introduction
Before we dive into the impact of feature engineering, let's briefly discuss why it is important. By engineering features, we aim to provide our models with more relevant and informative input data. This can help in capturing complex relationships and patterns in the data, leading to improved model performance.

## Data Preparation
To demonstrate the impact of feature engineering, we need a dataset to work with. We'll start by loading a dataset and performing some basic data preparation steps, such as handling missing values and encoding categorical variables.

```python
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import LabelEncoder

# Load dataset
data = pd.read_csv('data.csv')

# Split into features and target variable
X = data.drop('target', axis=1)
y = data['target']

# Encode categorical variables
categorical_cols = ['category1', 'category2']
encoder = LabelEncoder()

for col in categorical_cols:
    X[col] = encoder.fit_transform(X[col])

# Split into train and test sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
```

## Baseline Model
Before applying any feature engineering techniques, let's start by training a baseline model. This will serve as a reference point to compare our models with feature engineering.

```python
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score

# Train baseline model
baseline_model = LogisticRegression()
baseline_model.fit(X_train, y_train)

# Evaluate baseline model
baseline_preds = baseline_model.predict(X_test)
baseline_accuracy = accuracy_score(y_test, baseline_preds)
print(f"Baseline Model Accuracy: {baseline_accuracy}")
```

## Feature Engineering Techniques

### Scaling
One common feature engineering technique is scaling numerical features. This involves transforming numerical features into a consistent range to prevent features with larger values from dominating the learning process.

```python
from sklearn.preprocessing import StandardScaler

# Create scaler object and fit on training data
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)

# Apply the same scaling to test data
X_test_scaled = scaler.transform(X_test)
```

### Encoding Categorical Variables
Categorical variables need to be encoded to numeric form before feeding them into a machine learning model. One popular technique is one-hot encoding, where each category value is transformed into a binary feature.

```python
from sklearn.preprocessing import OneHotEncoder

# Initialize OneHotEncoder object
encoder = OneHotEncoder(handle_unknown='ignore', sparse=False)

# Fit and transform categorical features
X_train_encoded = encoder.fit_transform(X_train[categorical_cols])
X_test_encoded = encoder.transform(X_test[categorical_cols])
```

### Creating Interaction Terms
Interaction terms capture the combined effect of two or more features. This can be useful in capturing non-linear relationships between variables.

```python
from sklearn.preprocessing import PolynomialFeatures

# Create interaction terms for selected features
interaction_features = ['feature1', 'feature2']
poly = PolynomialFeatures(degree=2, include_bias=False)

# Transform selected features
X_train_interactions = poly.fit_transform(X_train[interaction_features])
X_test_interactions = poly.transform(X_test[interaction_features])
```

### Handling Missing Values
Missing values are a common problem in real-world datasets. One approach to handling missing values is imputation, where missing values are replaced with a sensible estimate. This ensures that the model can still learn from the available data.

```python
from sklearn.impute import SimpleImputer

# Initialize SimpleImputer object with strategy 'mean'
imputer = SimpleImputer(strategy='mean')

# Fit imputer on training data and apply to test data
X_train_imputed = imputer.fit_transform(X_train)
X_test_imputed = imputer.transform(X_test)
```

## Model Evaluation
After applying the feature engineering techniques, it's important to evaluate the impact on model performance. Let's train and evaluate a classifier model using the transformed features.

```python
# Train model on transformed features
model = LogisticRegression()
model.fit(X_train_transformed, y_train)

# Evaluate model on transformed test set
preds = model.predict(X_test_transformed)
accuracy = accuracy_score(y_test, preds)
print(f"Model Accuracy: {accuracy}")
```

## Conclusion
Feature engineering plays a vital role in improving the performance of machine learning models. By applying various techniques such as scaling, encoding categorical variables, creating interaction terms, and handling missing values, we can enhance the representation of our data and capture more complex relationships. It's essential to evaluate the impact of feature engineering on model performance to ensure that it leads to improved results.

By following the steps outlined in this blog post, you can explore different feature engineering techniques and gain insights into their impact on model performance. Remember, feature engineering is an iterative process, and experimentation is key to finding the best features for your models.

References:
- [Scikit-learn Documentation](https://scikit-learn.org/)
- [Feature Engineering for Machine Learning](https://www.oreilly.com/library/view/feature-engineering-for/9781491953235/) by Alice Zheng and Amanda Casari