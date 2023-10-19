---
layout: post
title: "[python] Building a basic neural network in Python"
description: " "
date: 2023-10-19
tags: [python]
comments: true
share: true
---

Neural networks are widely used in machine learning to model complex relationships and make predictions based on multiple inputs. In this tutorial, we will build a basic neural network using Python and the popular deep learning library, TensorFlow.

## Table of Contents
1. [Installation](#installation)
2. [Data Preparation](#data-preparation)
3. [Model Creation](#model-creation)
4. [Training](#training)
5. [Evaluation](#evaluation)
6. [Conclusion](#conclusion)

## 1. Installation <a name="installation"></a>

First, we need to install TensorFlow. You can install it using pip, the Python package installer, by running the following command:

```python
pip install tensorflow
```

## 2. Data Preparation <a name="data-preparation"></a>

To train our neural network, we need a dataset. In this example, we will use the classic MNIST dataset, which consists of 70,000 hand-written digits.

```python
import tensorflow as tf
from tensorflow.keras.datasets import mnist

# Load the MNIST dataset
(X_train, y_train), (X_test, y_test) = mnist.load_data()
```

## 3. Model Creation <a name="model-creation"></a>

Next, we will create our neural network model using TensorFlow's high-level API, Keras.

```python
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense, Flatten

# Create a sequential model
model = Sequential()

# Add a flatten layer to convert the input to a 1D array
model.add(Flatten(input_shape=(28, 28)))

# Add a fully connected dense layer with 128 units and ReLU activation
model.add(Dense(128, activation='relu'))

# Add an output layer with 10 units for the 10 possible digit labels
model.add(Dense(10, activation='softmax'))

# Compile the model
model.compile(optimizer='adam', loss='sparse_categorical_crossentropy', metrics=['accuracy'])
```

## 4. Training <a name="training"></a>

Now, we will train our model on the training data.

```python
# Train the model
model.fit(X_train, y_train, epochs=10, batch_size=32)
```

## 5. Evaluation <a name="evaluation"></a>

After training, we need to evaluate our model on the test data to measure its performance.

```python
# Evaluate the model
loss, accuracy = model.evaluate(X_test, y_test)
print(f"Test Loss: {loss}")
print(f"Test Accuracy: {accuracy}")
```

## 6. Conclusion <a name="conclusion"></a>

In this tutorial, we have built a basic neural network using Python and TensorFlow. We have covered the steps from installation to training and evaluation. Neural networks have a wide range of applications in machine learning, and this basic example can serve as a starting point for more complex projects.

**References:**
- [TensorFlow Documentation](https://www.tensorflow.org/)
- [Keras Documentation](https://keras.io/)
- [MNIST Dataset](http://yann.lecun.com/exdb/mnist/)