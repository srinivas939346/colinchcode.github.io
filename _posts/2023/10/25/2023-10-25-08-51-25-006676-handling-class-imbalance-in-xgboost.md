---
layout: post
title: "[python] Handling class imbalance in XGBoost"
description: " "
date: 2023-10-25
tags: [python]
comments: true
share: true
---

Class imbalance is a common occurrence in many machine learning problems, where the number of samples in one class significantly outweighs the number of samples in the other class. This can pose a challenge when training a model, as the model may tend to perform poorly on the minority class.

In this blog post, we will discuss how to handle class imbalance in XGBoost, a popular gradient boosting algorithm. We will explore two approaches: using class weights and resampling techniques.

### Using Class Weights

XGBoost allows us to assign weights to different classes during the training process. By assigning higher weights to the minority class samples, we can put more focus on correctly predicting these samples.

Here's an example of how to use class weights in XGBoost:

```python
import xgboost as xgb
from sklearn.datasets import make_classification
from sklearn.model_selection import train_test_split
from sklearn.metrics import classification_report

# Generate synthetic imbalanced dataset
X, y = make_classification(n_samples=1000, weights=[0.9, 0.1])

# Split the data into train and test sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

# Assign class weights
weights = [10, 1]  # higher weight for minority class

# Create DMatrix for XGBoost
dtrain = xgb.DMatrix(X_train, label=y_train, weight=[weights[y] for y in y_train])
dtest = xgb.DMatrix(X_test, label=y_test)

# Define the XGBoost parameters
params = {
    'objective': 'binary:logistic',
    'eval_metric': 'logloss'
}

# Train the XGBoost model
model = xgb.train(params, dtrain)

# Make predictions on test set
y_pred = model.predict(dtest)

# Evaluate the model
print(classification_report(y_test, y_pred.round()))
```

In this example, we first generate a synthetic imbalanced dataset using `make_classification` from scikit-learn. We then split the data into train and test sets. We assign class weights of 10 for the majority class and 1 for the minority class. When creating the `DMatrix` for XGBoost, we pass the weights corresponding to each sample in the `weight` parameter. Finally, we train the XGBoost model and evaluate its performance on the test set.

### Resampling Techniques

Another approach to handle class imbalance is by using resampling techniques. This involves either oversampling the minority class or undersampling the majority class to create a balanced training dataset.

Here's an example of how to use oversampling technique (specifically SMOTE) in XGBoost:

```python
import xgboost as xgb
from imblearn.over_sampling import SMOTE
from sklearn.datasets import make_classification
from sklearn.model_selection import train_test_split
from sklearn.metrics import classification_report

# Generate synthetic imbalanced dataset
X, y = make_classification(n_samples=1000, weights=[0.9, 0.1])

# Split the data into train and test sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

# Apply SMOTE oversampling
oversampler = SMOTE()
X_train_resampled, y_train_resampled = oversampler.fit_resample(X_train, y_train)

# Create DMatrix for XGBoost
dtrain = xgb.DMatrix(X_train_resampled, label=y_train_resampled)
dtest = xgb.DMatrix(X_test, label=y_test)

# Define the XGBoost parameters
params = {
    'objective': 'binary:logistic',
    'eval_metric': 'logloss'
}

# Train the XGBoost model
model = xgb.train(params, dtrain)

# Make predictions on test set
y_pred = model.predict(dtest)

# Evaluate the model
print(classification_report(y_test, y_pred.round()))
```

In this example, we again generate a synthetic imbalanced dataset using `make_classification`. After splitting the data into train and test sets, we apply SMOTE oversampling on the training data using `imblearn` library. SMOTE generates synthetic samples for the minority class to achieve a balanced dataset. We then create the `DMatrix` for XGBoost and train the model. Finally, we evaluate the model on the test set.

### Conclusion

Handling class imbalance is crucial to ensure accurate predictions in machine learning models. In this blog post, we discussed two approaches to handle class imbalance in XGBoost: using class weights and resampling techniques. Both methods can be effective in improving the model's performance on the minority class.