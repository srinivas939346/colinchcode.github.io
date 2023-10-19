---
layout: post
title: "[python] Regression with neural networks in Python"
description: " "
date: 2023-10-19
tags: [python]
comments: true
share: true
---

In this tutorial, we will explore how to perform regression using neural networks in Python. Regression is the process of predicting a continuous output variable based on one or more input variables. Neural networks, with their ability to model complex relationships, are well-suited for regression tasks.

## Prerequisites

To follow along with this tutorial, it is recommended to have basic knowledge of Python programming and familiarity with the concepts of neural networks. Additionally, you will need to have the following libraries installed:

- TensorFlow
- Keras
- NumPy
- Matplotlib

## The Dataset

To demonstrate regression with neural networks, let's use a sample dataset. Suppose we have data on the age and salary of employees. We want to build a neural network model that can predict the salary based on the age of an employee.

## Data Preprocessing

Before training the neural network, we need to preprocess the data. This may involve steps such as scaling the input features, splitting the data into training and testing sets, and normalizing the output variable.

```python
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import MinMaxScaler

# Load the dataset
data = np.loadtxt('salary_data.csv', delimiter=',')

# Separate input features and output variable
X = data[:, 0].reshape(-1, 1)  # age
y = data[:, 1].reshape(-1, 1)  # salary

# Scale the input features
scaler = MinMaxScaler()
X_scaled = scaler.fit_transform(X)

# Split the data into training and testing sets
X_train, X_test, y_train, y_test = train_test_split(X_scaled, y, test_size=0.2)
```

## Building the Neural Network Model

Now, let's build the neural network model using Keras. We will use a simple architecture with a single input layer, one hidden layer, and an output layer.

```python
from keras.models import Sequential
from keras.layers import Dense

# Create the model
model = Sequential()
model.add(Dense(8, input_dim=1, activation='relu'))  # hidden layer with 8 neurons
model.add(Dense(1, activation='linear'))  # output layer

# Compile the model
model.compile(loss='mean_squared_error', optimizer='adam')
```

## Training the Model

Next, we will train the neural network model using the training data. We will specify the number of epochs (iterations) and the batch size.

```python
model.fit(X_train, y_train, epochs=50, batch_size=32)
```

## Evaluating the Model

Once the model is trained, we can evaluate its performance using the testing data.

```python
loss = model.evaluate(X_test, y_test)
print(f"Mean Squared Error: {loss}")
```

## Making Predictions

Finally, we can use the trained model to make predictions on new data.

```python
# Suppose we want to predict the salary for an employee aged 35
age = np.array([[35]])
scaled_age = scaler.transform(age)
predicted_salary = model.predict(scaled_age)
print(f"Predicted Salary: {predicted_salary[0][0]}")
```

## Conclusion

In this tutorial, we learned how to perform regression using neural networks in Python. By preprocessing the data, building the neural network model, training it, and making predictions, we can leverage the power of neural networks to predict continuous output variables accurately. Neural networks offer a flexible and powerful approach to regression tasks, allowing us to model complex relationships between input and output variables.

## References

- TensorFlow documentation: [https://www.tensorflow.org](https://www.tensorflow.org)
- Keras documentation: [https://keras.io](https://keras.io)
- NumPy documentation: [https://numpy.org/doc/](https://numpy.org/doc/)
- Matplotlib documentation: [https://matplotlib.org/stable/contents.html](https://matplotlib.org/stable/contents.html)