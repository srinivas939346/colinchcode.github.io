---
layout: post
title: "[python] Image classification using Keras"
description: " "
date: 2023-10-23
tags: [python]
comments: true
share: true
---

In this tutorial, we will learn how to build an image classifier using Keras, a high-level neural networks library in Python. We will use a convolutional neural network (CNN) to classify images.

## Table of Contents
- [Introduction to Image Classification](#introduction-to-image-classification)
- [Setting up the Environment](#setting-up-the-environment)
- [Loading and Preprocessing the Data](#loading-and-preprocessing-the-data)
- [Building the CNN Model](#building-the-cnn-model)
- [Training the Model](#training-the-model)
- [Evaluating the Model](#evaluating-the-model)
- [Conclusion](#conclusion)
- [References](#references)

## Introduction to Image Classification

Image classification is the process of categorizing images into different classes or labels. It is a popular task in computer vision and finds applications in various domains such as autonomous driving, healthcare, and security.

## Setting up the Environment

To get started, we need to set up the environment by installing the necessary libraries. We will need Python, Keras, and TensorFlow.

```python
pip install keras tensorflow
```

## Loading and Preprocessing the Data

For this tutorial, we will use the CIFAR-10 dataset, which consists of 60,000 images divided into 10 classes. Keras provides a convenient API to load this dataset.

```python
from keras.datasets import cifar10

(X_train, y_train), (X_test, y_test) = cifar10.load_data()
```

Next, we need to preprocess the data by normalizing pixel values and converting labels to categorical format.

```python
from keras.utils import to_categorical

# Normalize pixel values
X_train = X_train / 255.0
X_test = X_test / 255.0

# Convert labels to categorical format
y_train = to_categorical(y_train, num_classes=10)
y_test = to_categorical(y_test, num_classes=10)
```

## Building the CNN Model

A CNN is a type of neural network that is particularly effective in image classification tasks. We will build a simple CNN model using Keras.

```python
from keras.models import Sequential
from keras.layers import Conv2D, MaxPooling2D, Flatten, Dense

model = Sequential()

model.add(Conv2D(32, (3, 3), activation='relu', input_shape=(32, 32, 3)))
model.add(MaxPooling2D((2, 2)))

model.add(Flatten())

model.add(Dense(64, activation='relu'))
model.add(Dense(10, activation='softmax'))
```

The model consists of two convolutional layers, followed by max pooling and a fully connected layer. The output layer uses the softmax activation function for multi-class classification.

## Training the Model

To train the model, we need to compile it with an optimizer, define the loss function, and specify the metrics we want to track during training.

```python
model.compile(optimizer='adam', loss='categorical_crossentropy', metrics=['accuracy'])

model.fit(X_train, y_train, batch_size=128, epochs=10, validation_data=(X_test, y_test))
```

## Evaluating the Model

After training, we can evaluate the model's performance on the test set.

```python
loss, accuracy = model.evaluate(X_test, y_test)
print("Test accuracy:", accuracy)
```

## Conclusion

In this tutorial, we have learned how to build an image classifier using Keras. We explored the steps involved in loading, preprocessing, building, training, and evaluating a CNN model for image classification. With this knowledge, you can now apply image classification techniques to your own projects.

## References

- [Keras Documentation](https://keras.io/)
- [TensorFlow Documentation](https://www.tensorflow.org/)