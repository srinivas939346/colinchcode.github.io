---
layout: post
title: "[python] Saving and loading XGBoost models"
description: " "
date: 2023-10-25
tags: [python]
comments: true
share: true
---

XGBoost is a popular open-source library for gradient boosting, known for its efficiency and performance. Once you've trained an XGBoost model, you'll often want to save it for later use or share it with others. In this blog post, we'll explore how to save and load XGBoost models using Python.

## Table of Contents

- [Saving the Model](#saving-the-model)
- [Loading the Model](#loading-the-model)
- [Usage Example](#usage-example)
- [Conclusion](#conclusion)

## Saving the Model

To save an XGBoost model, you can use the `save_model` function provided by the library. This function takes two arguments - the trained model and the file path where you want to save it.

Here's an example of how to save an XGBoost model:

```python
import xgboost as xgb

# Train an XGBoost model
model = xgb.XGBRegressor()
model.fit(X_train, y_train)

# Save the trained model
model.save_model('path/to/model.xgb')
```

In the above code, we train an XGBoost model using some training data. Then, we call the `save_model` function on the trained model and specify the file path where we want to save it.

## Loading the Model

To load a saved XGBoost model, you can use the `load_model` function provided by the library. This function takes the file path of the saved model as an argument and returns the loaded model.

Here's an example of how to load a saved XGBoost model:

```python
import xgboost as xgb

# Load the saved model
loaded_model = xgb.Booster()
loaded_model.load_model('path/to/model.xgb')

# Use the loaded model for prediction
predictions = loaded_model.predict(X_test)
```

In the above code, we first create an empty XGBoost model using the `Booster` class. Then, we call the `load_model` function on the empty model and specify the file path of the saved model.

## Usage Example

Let's see a complete example of saving and loading an XGBoost model using a regression task:

```python
import xgboost as xgb
from sklearn.datasets import load_boston
from sklearn.model_selection import train_test_split

# Load the Boston Housing dataset
data = load_boston()
X_train, X_test, y_train, y_test = train_test_split(data.data, data.target, test_size=0.2, random_state=42)

# Train an XGBoost model
model = xgb.XGBRegressor()
model.fit(X_train, y_train)

# Save the trained model
model.save_model('path/to/model.xgb')

# Load the saved model
loaded_model = xgb.Booster()
loaded_model.load_model('path/to/model.xgb')

# Use the loaded model for prediction
predictions = loaded_model.predict(X_test)
```

In this example, we load the Boston Housing dataset, split it into training and testing sets, and then train an XGBoost regression model on the training data. We save the trained model using `save_model` and then load it later using `load_model`. Finally, we make predictions on the testing data using the loaded model.

## Conclusion

Saving and loading XGBoost models is a simple and straightforward process. By utilizing the `save_model` and `load_model` functions provided by the XGBoost library, you can easily save and load your trained models for future use or sharing with others.