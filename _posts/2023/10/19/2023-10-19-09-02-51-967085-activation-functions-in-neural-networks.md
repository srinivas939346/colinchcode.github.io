---
layout: post
title: "[python] Activation functions in neural networks"
description: " "
date: 2023-10-19
tags: [python]
comments: true
share: true
---

Activation functions play a crucial role in neural networks by introducing non-linearity into the model and allowing it to learn complex patterns. In this blog post, we will explore some commonly used activation functions in neural networks and their properties.

## Table of Contents

1. [Introduction](#introduction)
2. [Sigmoid](#sigmoid)
3. [ReLU](#relu)
4. [Tanh](#tanh)
5. [Conclusion](#conclusion)

## Introduction

Activation functions determine the output of a neuron given its input. They are applied element-wise to the output of each neuron in the neural network. The choice of activation function depends on the problem at hand and can significantly affect the model's performance.

## Sigmoid

The sigmoid function, also known as the logistic function, is a commonly used activation function. It maps the input to a value between 0 and 1, representing the probability of the neuron being activated. The formula for the sigmoid function is:

```
sigmoid(x) = 1 / (1 + exp(-x))
```

Some key properties of the sigmoid function include:

- It is differentiable, which allows for efficient training using gradient-based optimization algorithms.
- It squashes the input to a limited range, which can help prevent exploding gradients in deep neural networks.
- However, it suffers from the "vanishing gradient" problem, where gradients become very small for large input values, leading to slow convergence or no learning at all.

## ReLU

ReLU (Rectified Linear Unit) is another widely used activation function that overcomes the vanishing gradient problem. It returns x if x is positive, and 0 otherwise. The formula for the ReLU function is:

```
ReLU(x) = max(0, x)
```

Key properties of ReLU include:

- It is computationally efficient to calculate, making it suitable for large-scale neural networks.
- It does not suffer from the vanishing gradient problem since it does not saturate for positive inputs.
- However, ReLU can cause dead neurons, where neurons become inactive and do not contribute to the learning process. This can be mitigated by using variants such as Leaky ReLU or Parametric ReLU.

## Tanh

The hyperbolic tangent function, commonly known as tanh, is a scaled version of the sigmoid function that outputs values between -1 and 1. The formula for the tanh function is:

```
tanh(x) = (exp(x) - exp(-x)) / (exp(x) + exp(-x))
```

Some key properties of the tanh function include:

- It is zero-centered, which can aid in training the model.
- Like the sigmoid function, it suffers from the vanishing gradient problem for large inputs.

## Conclusion

Activation functions are an integral part of neural networks that introduce non-linearity and allow for learning complex patterns. The choice of activation function should be based on the specific problem and the characteristics of the function. Sigmoid, ReLU, and tanh are just a few examples of many available activation functions, each with its own advantages and limitations.

Remember to experiment and see which activation function works best for your neural network model. Happy coding!

References:
- [Deep Learning](http://www.deeplearningbook.org)
- [CS231n: Convolutional Neural Networks for Visual Recognition](http://cs231n.github.io/neural-networks-1)
- [Activation Functions in Neural Networks](https://towardsdatascience.com/activation-functions-neural-networks-1cbd9f8d91d6)