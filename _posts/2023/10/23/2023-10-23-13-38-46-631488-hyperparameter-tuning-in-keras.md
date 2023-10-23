---
layout: post
title: "[python] Hyperparameter tuning in Keras"
description: " "
date: 2023-10-23
tags: [python]
comments: true
share: true
---

Hyperparameter tuning is an important step in machine learning model development to optimize the performance of the model. In this tutorial, we will explore how to perform hyperparameter tuning in Keras, a popular deep learning library in Python.

## Table of Contents

- [What are hyperparameters?](#what-are-hyperparameters)
- [Hyperparameter tuning techniques](#hyperparameter-tuning-techniques)
- [Grid search](#grid-search)
- [Random search](#random-search)
- [Bayesian optimization](#bayesian-optimization)
- [Conclusion](#conclusion)
- [References](#references)

## What are hyperparameters?

Hyperparameters are the configuration settings of a machine learning model that are set before training and affect the learning process. They are not learned from the data but are determined by the data scientist or machine learning engineer.

Some common hyperparameters in deep learning models include learning rate, batch size, number of epochs, optimizer choice, and regularization strength. Tuning these hyperparameters can have a significant impact on the model's performance.

## Hyperparameter tuning techniques

There are several techniques available for hyperparameter tuning, including grid search, random search, and Bayesian optimization. In this tutorial, we will focus on these three techniques.

### Grid search

Grid search is a brute-force approach to hyperparameter tuning. It involves defining a grid of possible hyperparameter values and exhaustively searching through all combinations to find the best set of hyperparameters.

Here's an example of how to perform grid search in Keras using the `GridSearchCV` class from scikit-learn:

```python
from sklearn.model_selection import GridSearchCV
from keras.wrappers.scikit_learn import KerasClassifier

def create_model(optimizer='adam'):
    model = Sequential()
    # Add layers to the model
    return model

# Define hyperparameters and their possible values
hyperparameters = {
    'optimizer': ['adam', 'sgd'],
    'batch_size': [16, 32, 64],
    'epochs': [10, 20, 30]
}

# Create the Keras model
model = KerasClassifier(build_fn=create_model)

# Perform grid search
grid = GridSearchCV(estimator=model, param_grid=hyperparameters, cv=3)
grid_result = grid.fit(X, y)

# Print the best hyperparameters and associated score
print("Best hyperparameters:", grid_result.best_params_)
print("Best score:", grid_result.best_score_)
```

### Random search

Random search is another approach to hyperparameter tuning where random combinations of hyperparameters are selected and evaluated. It is less computationally expensive than grid search but can still find good hyperparameter values.

Here's an example of how to perform random search in Keras using the `RandomizedSearchCV` class from scikit-learn:

```python
from sklearn.model_selection import RandomizedSearchCV
from keras.wrappers.scikit_learn import KerasClassifier

def create_model(optimizer='adam'):
    model = Sequential()
    # Add layers to the model
    return model

# Define hyperparameters and their possible values
hyperparameters = {
    'optimizer': ['adam', 'sgd'],
    'batch_size': [16, 32, 64],
    'epochs': [10, 20, 30]
}

# Create the Keras model
model = KerasClassifier(build_fn=create_model)

# Perform random search
random = RandomizedSearchCV(estimator=model, param_distributions=hyperparameters, cv=3)
random_result = random.fit(X, y)

# Print the best hyperparameters and associated score
print("Best hyperparameters:", random_result.best_params_)
print("Best score:", random_result.best_score_)
```

### Bayesian optimization

Bayesian optimization is a more advanced technique that uses probabilistic models to model the performance of hyperparameter configurations and selects the most promising configurations to evaluate.

There are several Python libraries available for Bayesian optimization, such as `hyperopt`, `Optuna`, and `scikit-optimize`. Here's an example of how to perform Bayesian optimization using `hyperopt`:

```python
from hyperopt import Trials, STATUS_OK, tpe, hp, fmin
from keras.models import Sequential
# Add other necessary import statements

space = {
    'optimizer': hp.choice('optimizer', ['adam', 'sgd']),
    'batch_size': hp.choice('batch_size', [16, 32, 64]),
    'epochs': hp.choice('epochs', [10, 20, 30])
}

def objective(params):
    model = Sequential()
    # Add layers to the model
    # Set hyperparameters
    model.compile(...)
    model.fit(...)
    # Calculate evaluation metric
    return {'loss': metric_value, 'status': STATUS_OK}

trials = Trials()
best = fmin(fn=objective, space=space, algo=tpe.suggest, max_evals=100, trials=trials)

# Print the best hyperparameters
print("Best hyperparameters:", best)
```

## Conclusion

In this tutorial, we explored three popular techniques for hyperparameter tuning in Keras: grid search, random search, and Bayesian optimization. By tuning the hyperparameters of our models, we can significantly improve their performance. It is recommended to combine these techniques with cross-validation to prevent overfitting and obtain reliable model performance estimations.

Hyperparameter tuning is an iterative process, and there is no one-size-fits-all approach. It requires experimentation and domain expertise to find the best set of hyperparameters for a specific problem.