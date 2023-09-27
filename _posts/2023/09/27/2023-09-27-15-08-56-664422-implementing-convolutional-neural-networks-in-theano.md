---
layout: post
title: "[python] Implementing convolutional neural networks in Theano"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---

Convolutional Neural Networks (CNNs) have revolutionized the field of computer vision and are widely used for tasks like image classification, object detection, and image segmentation. Theano is a popular deep learning library that allows us to efficiently define, optimize, and evaluate mathematical expressions involving multi-dimensional arrays.

In this post, we will walk through the steps of implementing a CNN using Theano. We will focus on creating and training a simple CNN for image classification.

## Table of Contents

- [What is a Convolutional Neural Network (CNN)?](#what-is-a-convolutional-neural-network-cnn)
- [Setting up Theano](#setting-up-theano)
- [Implementing the CNN](#implementing-the-cnn)
- [Training the CNN](#training-the-cnn)
- [Conclusion](#conclusion)

## What is a Convolutional Neural Network (CNN)?

A Convolutional Neural Network (CNN) is a type of deep learning model that is specifically designed to process and analyze visual data. It consists of multiple layers including convolutional layers, pooling layers, and fully connected layers. CNNs are highly effective in capturing local spatial dependencies in images, making them capable of handling complex visual recognition tasks.

## Setting up Theano

To get started, make sure you have Theano installed on your system. You can install it using pip:

```
pip install Theano
```

Once Theano is installed, you can import it in your Python script:

```python
import theano
```

## Implementing the CNN

Let's now define the architecture of our CNN. We will create a simple CNN with two convolutional layers followed by a fully connected layer.

```python
import theano.tensor as T
from theano.tensor.signal import pool

# Define the input variables
x = T.tensor4('x')

# Define the first convolutional layer
filter1 = theano.shared(np.random.randn(num_filters1, num_channels, filter_size, filter_size), name='filter1')
conv1 = T.nnet.conv2d(x, filter1)

# Apply a non-linear activation function (e.g., ReLU)
conv1_activation = T.maximum(conv1, 0)

# Apply max pooling to downsample the feature maps
pooled1 = pool.pool_2d(conv1_activation, (2, 2), ignore_border=True)
```

In this example, `x` is the input tensor, `num_filters1` is the number of filters in the first convolutional layer, `num_channels` is the number of input channels, `filter_size` is the size of the filters, `filter1` is a shared variable representing the filter values, `conv1` is the output of the convolution operation, `conv1_activation` applies the ReLU activation function, and `pooled1` performs max pooling on the feature maps.

## Training the CNN

To train our CNN, we need a labeled dataset. We will use the popular MNIST dataset for this purpose. The MNIST dataset consists of 60,000 training examples and 10,000 test examples of handwritten digits.

We can use Theano's built-in functions to define the loss function, optimize it using gradient descent, and train the network on the MNIST dataset.

```python
import theano.tensor as T
from theano.tensor.nnet import softmax
from theano import function

# Define the output variables
y = T.matrix('y')

# Define the second convolutional layer
filter2 = theano.shared(np.random.randn(num_filters2, num_filters1, filter_size, filter_size), name='filter2')
conv2 = T.nnet.conv2d(pooled1, filter2)

# Flatten the output of the second convolutional layer
flattened = T.flatten(conv2, outdim=2)

# Define the fully connected layer
W = theano.shared(np.random.randn(num_filters2 * (input_size // 2) * (input_size // 2), num_classes), name='W')
b = theano.shared(np.zeros((num_classes,)), name='b')
output = T.dot(flattened, W) + b

# Compute the softmax probabilities
probs = softmax(output)

# Define the loss function (e.g., cross-entropy)
loss = T.nnet.categorical_crossentropy(probs, y).mean()

# Define the updates for gradient descent
params = [filter1, filter2, W, b]
grads = T.grad(loss, params)
updates = [(param, param - learning_rate * grad) for param, grad in zip(params, grads)]

# Compile the training function
train = function(inputs=[x, y], outputs=loss, updates=updates)

# Train the CNN on the MNIST dataset
for epoch in range(num_epochs):
    for batch in iterate_minibatches(X_train, y_train, batch_size):
        loss_value = train(batch[0], batch[1])
        print('Epoch %d, loss=%f' % (epoch, loss_value))
```

In this example, `y` represents the true labels of the images, `filter2` is the weight matrix of the second convolutional layer, `conv2` is the output of the second convolution operation, `flattened` is the flattened version of `conv2` to be used as input to the fully connected layer, `W` and `b` are the weight and bias variables of the fully connected layer, `output` is the output of the fully connected layer, `probs` are the softmax probabilities, `loss` is the cross-entropy loss function, `params` are the parameters to be optimized, `grads` are the gradients of the loss with respect to `params`, `updates` apply the gradient descent updates to `params`, `train` is the compiled training function, and `iterate_minibatches` is a helper function that generates mini-batches of data from the training set.

## Conclusion

In this post, we have implemented a simple Convolutional Neural Network using Theano. We have defined the architecture of the CNN, including the layers and activation functions, and trained it on the MNIST dataset. Theano provides efficient tools for building and optimizing deep learning models, making it a popular choice among researchers and practitioners in the field of deep learning.

Remember to experiment with different architectures, hyperparameters, and datasets to further improve the performance of your CNN. Happy coding!