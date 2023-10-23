---
layout: post
title: "[python] Multi-GPU training in Keras"
description: " "
date: 2023-10-23
tags: [python]
comments: true
share: true
---

Training deep learning models can be computationally expensive, especially when dealing with large datasets and complex architectures. To accelerate the training process, we can leverage multiple GPUs to distribute the workload. In this blog post, we will explore how to perform multi-GPU training in Keras.

## Table of Contents
1. [Introduction](#introduction)
2. [Environment Setup](#environment-setup)
3. [Data Preparation](#data-preparation)
4. [Model Definition](#model-definition)
5. [Multi-GPU Training](#multi-gpu-training)
6. [Conclusion](#conclusion)

## Introduction <a name="introduction"></a>

Keras is a popular deep learning framework known for its simplicity and flexibility. It provides a high-level API for building and training neural networks, making it an excellent choice for this task. To utilize multiple GPUs in Keras, we need to use the `tf.distribute.MirroredStrategy` class provided by TensorFlow.

## Environment Setup <a name="environment-setup"></a>

Before diving into multi-GPU training, let's make sure our environment is properly set up. Ensure you have the following prerequisites installed:

- TensorFlow: `pip install tensorflow`
- Keras: `pip install keras`

Additionally, make sure you have multiple GPUs available on your machine.

## Data Preparation <a name="data-preparation"></a>

To demonstrate multi-GPU training, we will use the CIFAR-10 dataset, which consists of 50,000 training images and 10,000 test images belonging to 10 different classes. We can easily load this dataset using Keras:

```python
from keras.datasets import cifar10

(x_train, y_train), (x_test, y_test) = cifar10.load_data()
```

## Model Definition <a name="model-definition"></a>

Let's define a simple convolutional neural network (CNN) model for image classification:

```python
from keras.models import Sequential
from keras.layers import Conv2D, MaxPooling2D, Flatten, Dense

def build_model():
    model = Sequential()
    model.add(Conv2D(32, (3, 3), activation='relu', padding='same', input_shape=(32, 32, 3)))
    model.add(MaxPooling2D(pool_size=(2, 2)))
    model.add(Conv2D(64, (3, 3), activation='relu', padding='same'))
    model.add(MaxPooling2D(pool_size=(2, 2)))
    model.add(Flatten())
    model.add(Dense(64, activation='relu'))
    model.add(Dense(10, activation='softmax'))
    return model

model = build_model()
model.compile(optimizer='adam', loss='sparse_categorical_crossentropy', metrics=['accuracy'])
```

## Multi-GPU Training <a name="multi-gpu-training"></a>

To perform multi-GPU training, we need to wrap the model inside a `tf.distribute.MirroredStrategy` scope. This strategy creates copies of the model on each GPU, splits the input data across GPUs, and synchronizes gradients during the backpropagation phase.

```python
import tensorflow as tf

strategy = tf.distribute.MirroredStrategy()
with strategy.scope():
    model = build_model()
    model.compile(optimizer='adam', loss='sparse_categorical_crossentropy', metrics=['accuracy'])

model.fit(x_train, y_train, epochs=10, validation_data=(x_test, y_test))
```

That's it! Keras, with the help of TensorFlow, takes care of distributing the workload across multiple GPUs transparently.

## Conclusion <a name="conclusion"></a>

In this blog post, we have explored how to perform multi-GPU training in Keras. By leveraging the `tf.distribute.MirroredStrategy` class, we can easily distribute the training workload across multiple GPUs, speeding up the training process. This technique is especially useful when dealing with large datasets and complex models.

References:
- [Keras documentation](https://keras.io/)
- [TensorFlow documentation](https://www.tensorflow.org/)