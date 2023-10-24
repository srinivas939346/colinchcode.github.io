---
layout: post
title: "[python] Multi-class classification in XGBoost"
description: " "
date: 2023-10-25
tags: [python]
comments: true
share: true
---

XGBoost is a popular gradient boosting algorithm that is widely used for both regression and classification tasks. While it is commonly known for its effectiveness in binary classification problems, it can also be used for multi-class classification. In this blog post, we will explore how to perform multi-class classification using XGBoost in Python.

### Data Preparation

Before diving into the implementation, let's first prepare our data. In a multi-class classification problem, we have multiple classes or labels that we want to predict. It is crucial to one-hot encode the target variable to prepare it for multi-class classification. 

```python
# Import necessary libraries
import pandas as pd
from sklearn.preprocessing import OneHotEncoder

# Load the dataset
data = pd.read_csv("data.csv")

# Separate features and target variable
X = data.drop("target", axis=1)
y = data["target"]

# One-hot encode the target variable
one_hot_encoder = OneHotEncoder()
y_encoded = one_hot_encoder.fit_transform(y.to_frame())
```

### Training the XGBoost Model

After preparing the data, we can move on to training the XGBoost model. XGBoost provides a straightforward way to handle multi-class classification using the `multi:softmax` objective function. We also need to specify the `num_class` parameter to indicate the number of classes in our data. 

```python
import xgboost as xgb
from sklearn.model_selection import train_test_split

# Split the data into training and testing sets
X_train, X_test, y_train, y_test = train_test_split(X, y_encoded, test_size=0.2, random_state=42)

# Convert the datasets into XGBoost's DMatrix format
train_data = xgb.DMatrix(X_train, label=y_train)
test_data = xgb.DMatrix(X_test, label=y_test)

# Define the parameters for the XGBoost model
params = {
    "objective": "multi:softmax",
    "num_class": len(y.unique()),
}

# Train the XGBoost model
model = xgb.train(params, train_data, num_boost_round=10)

# Predict the classes for the test data
y_pred = model.predict(test_data)
```

### Evaluating the Model

Once we have trained the model and made predictions on the test data, we can evaluate its performance using various metrics. Since we are dealing with multi-class classification, it is important to use appropriate evaluation metrics such as accuracy, precision, recall, and F1-score.

```python
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score

# Convert the predicted classes back to original labels
y_pred_labels = one_hot_encoder.inverse_transform(pd.get_dummies(y_pred.reshape(-1, 1)))

# Calculate evaluation metrics
accuracy = accuracy_score(y_test, y_pred_labels)
precision = precision_score(y_test, y_pred_labels, average='weighted')
recall = recall_score(y_test, y_pred_labels, average='weighted')
f1 = f1_score(y_test, y_pred_labels, average='weighted')

print("Accuracy: {:.2f}".format(accuracy))
print("Precision: {:.2f}".format(precision))
print("Recall: {:.2f}".format(recall))
print("F1-score: {:.2f}".format(f1))
```

### Conclusion

In this blog post, we have learned how to perform multi-class classification using XGBoost in Python. We have covered the steps for data preparation, training the XGBoost model, and evaluating its performance. XGBoost provides powerful tools for multi-class classification tasks and can be a valuable addition to your machine learning toolbox.