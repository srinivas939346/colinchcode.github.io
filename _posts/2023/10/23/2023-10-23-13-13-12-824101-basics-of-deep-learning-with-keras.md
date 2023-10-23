---
layout: post
title: "[python] Basics of deep learning with Keras"
description: " "
date: 2023-10-23
tags: [python]
comments: true
share: true
---

Deep learning is a subfield of artificial intelligence that focuses on developing algorithms inspired by the structure and function of the human brain. It has gained popularity in recent years due to its ability to solve complex problems such as image and speech recognition, natural language processing, and many more. Keras, a high-level neural networks API, provides a user-friendly interface to build and train deep learning models. In this blog post, we will walk through the basics of deep learning with Keras.

## Table of Contents
- [Introduction to Deep Learning](#introduction-to-deep-learning)
- [Getting Started with Keras](#getting-started-with-keras)
- [Building a Neural Network](#building-a-neural-network)
- [Training and Evaluating the Model](#training-and-evaluating-the-model)
- [Conclusion](#conclusion)

## Introduction to Deep Learning

Deep learning involves training artificial neural networks with multiple layers of interconnected nodes, known as neurons. These neurons mimic the biological neurons in our brains and are responsible for learning patterns and making predictions. The deep neural network architecture enables the model to learn hierarchical representations of data, leading to improved accuracy and performance.

## Getting Started with Keras

To get started with Keras, you first need to install it by running `pip install keras`. Keras sits on top of other deep learning libraries like TensorFlow and Theano, making it compatible with a wide range of hardware and software configurations. Once installed, you can import the necessary libraries and start building your models.

## Building a Neural Network

Keras provides a simple and intuitive way to build neural networks. You start by defining the architecture of the network by stacking layers on top of each other. The input layer specifies the shape of the input data, and subsequent hidden layers apply various transformations to learn meaningful features. Finally, the output layer produces the desired predictions.

Here's an example of building a simple neural network with one input layer, two hidden layers, and one output layer using Keras:

```python
import keras
from keras.models import Sequential
from keras.layers import Dense

# Create a sequential model
model = Sequential()

# Add an input layer with 10 neurons
model.add(Dense(10, input_shape=(784,)))

# Add two hidden layers with 20 neurons each
model.add(Dense(20))
model.add(Dense(20))

# Add an output layer with 1 neuron
model.add(Dense(1))

# Print the model summary
model.summary()
```

In this example, we create a sequential model using `Sequential()` and add layers using `model.add()`. The `Dense` layer represents a fully connected layer where each neuron is connected to every neuron in the previous layer.

## Training and Evaluating the Model

After defining the model architecture, you need to compile it with the appropriate loss function, optimizer, and metrics before training. The loss function measures the deviation between predicted and actual values, and the optimizer adjusts the model's weights to minimize the loss. During training, you provide input data and target labels to the model and let it learn.

Here's an example of compiling and training the model:

```python
# Compile the model
model.compile(loss='mse', optimizer='adam', metrics=['mae'])

# Train the model
model.fit(x_train, y_train, batch_size=32, epochs=10, validation_data=(x_val, y_val))

# Evaluate the model
loss, accuracy = model.evaluate(x_test, y_test)

print(f"Test loss: {loss}")
print(f"Test accuracy: {accuracy}")
```
In this example, we compile the model with mean squared error (`mse`) as the loss function and Adam optimizer. The metrics parameter specifies the evaluation metric to track during training. We then train the model using the `fit()` method, providing training data, batch size, number of epochs, and validation data. Finally, we evaluate the model's performance on the test data using the `evaluate()` method.

## Conclusion

Keras simplifies the process of building and training deep learning models. It abstracts away the complexities of lower-level frameworks and allows you to focus on the architecture and design of your neural networks. In this blog post, we covered the basics of deep learning with Keras, starting from an introduction to deep learning to building and training a simple neural network. As you explore further, you'll discover the vast possibilities that deep learning can offer in solving complex problems.

## References

1. [Keras Documentation](https://keras.io/)
2. [Deep Learning with Python by Francois Chollet](https://www.manning.com/books/deep-learning-with-python)