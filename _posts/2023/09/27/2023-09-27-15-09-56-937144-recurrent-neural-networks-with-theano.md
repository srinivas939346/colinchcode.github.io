---
layout: post
title: "[python] Recurrent neural networks with Theano"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---

Recurrent Neural Networks (RNNs) are a type of deep learning model that are well-suited for sequential data such as time series or natural language processing tasks. Theano is a popular Python library that allows us to efficiently define and train neural networks. In this tutorial, we will explore how to implement RNNs using Theano.

## Table of Contents
1. Introduction to Recurrent Neural Networks
2. Theano: An Introduction
3. Creating the RNN Architecture
4. Training the RNN model
5. Making Predictions with the RNN
6. Conclusion

## 1. Introduction to Recurrent Neural Networks

Recurrent Neural Networks are a type of neural network that have loops within their architecture, allowing them to maintain an internal memory of past inputs. This makes them particularly effective in capturing the sequential nature of data. 

RNNs have become popular in various applications such as language modeling, speech recognition, machine translation, and sentiment analysis. They are known for their ability to handle variable-length inputs and generate variable-length outputs.

## 2. Theano: An Introduction

Theano is a powerful numerical computation library in Python that enables us to efficiently define, optimize, and evaluate mathematical expressions, especially those involving multi-dimensional arrays. It provides a flexible yet efficient framework for building and training neural networks.

To install Theano, you can use pip:

```
pip install theano
```

## 3. Creating the RNN Architecture

To build a recurrent neural network with Theano, we first need to define the architecture. This includes specifying the number of hidden units, number of input features, and any additional layers such as embedding layers or output layers.

```python
import theano
import theano.tensor as T
import numpy as np

class RNN:
    def __init__(self, input_size, hidden_size, output_size):
        self.input_size = input_size
        self.hidden_size = hidden_size
        self.output_size = output_size
        
        self.Wxh = theano.shared(np.random.randn(hidden_size, input_size) * 0.01) 
        self.Whh = theano.shared(np.random.randn(hidden_size, hidden_size) * 0.01)
        self.Why = theano.shared(np.random.randn(output_size, hidden_size) * 0.01)
        self.bh = theano.shared(np.zeros(hidden_size))
        self.by = theano.shared(np.zeros(output_size))
        
        self.params = [self.Wxh, self.Whh, self.Why, self.bh, self.by]
        
        # Define the input and output variables
        self.x = T.matrix("x")
        self.y = T.matrix("y")
```

Here, we have defined a class `RNN` that represents the RNN architecture. We initialize the class with the input size, hidden size, and output size. We then create the required weight matrices and bias vectors using `theano.shared`. Finally, we define the input and output variables.

## 4. Training the RNN model

Once we have defined the architecture, we can proceed to train the RNN model. Training involves forward propagation, backpropagation, and model updates using an optimization algorithm such as gradient descent.

Below is the code for the `train` method of our `RNN` class:

```python
class RNN:
    ...
    def train(self, input_sequence, target_sequence, learning_rate=0.1, num_epochs=100):
        x = self.x
        y = self.y

        # Forward Propagation
        hidden_state, _ = theano.scan(
            fn=self.forward_step,
            sequences=[x],
            outputs_info=[T.zeros(self.hidden_size)]
        )
        
        output = T.nnet.softmax(T.dot(self.Why, hidden_state[-1]) + self.by)[0]
        
        # Loss function
        loss = T.nnet.categorical_crossentropy(output, y).mean()
        
        # Backpropagation
        grads = T.grad(loss, self.params)
        updates = [(param_i, param_i - learning_rate * grad_i) for param_i, grad_i in zip(self.params, grads)]
        
        # Compile the training function
        train_fn = theano.function(
            inputs=[x, y],
            outputs=[loss],
            updates=updates,
            allow_input_downcast=True
        )
        
        # Train the model
        for epoch in range(num_epochs):
            loss = train_fn(input_sequence, target_sequence)
            print(f"Epoch {epoch+1}/{num_epochs}, Loss: {loss}")
```

In this code snippet, we define the forward propagation step using `theano.scan`, which allows us to apply the `forward_step` function to each input in the sequence. We then compute the output using the weights and biases, and calculate the loss function. Finally, we use backpropagation to compute the gradients and update the parameters.

## 5. Making Predictions with the RNN

Once the model is trained, we can use it to make predictions. This involves running the forward propagation step and obtaining the output probabilities. We can then select the prediction with the highest probability as the predicted class.

```python
class RNN:
    ...
    def predict(self, input_sequence):
        x = self.x
        
        # Forward Propagation
        hidden_state, _ = theano.scan(
            fn=self.forward_step,
            sequences=[x],
            outputs_info=[T.zeros(self.hidden_size)]
        )
        
        output = T.nnet.softmax(T.dot(self.Why, hidden_state[-1]) + self.by)[0]
        
        # Compile the prediction function
        predict_fn = theano.function(
            inputs=[x],
            outputs=[output],
            allow_input_downcast=True
        )
        
        # Run the model on input sequence
        prediction = predict_fn(input_sequence)
        return np.argmax(prediction)
```

In this code snippet, we define the predict function which performs the forward propagation step and returns the predicted class. We use `theano.scan` to apply the `forward_step` function to each input in the sequence and compute the output probabilities.

## 6. Conclusion

In this tutorial, we have seen how to implement Recurrent Neural Networks using Theano. We have learned how to define the architecture, train the model, and make predictions. RNNs are a powerful tool for modeling sequential data and Theano provides an efficient way to build and train these models. With the knowledge gained from this tutorial, you can now explore more advanced RNN architectures and use them in various applications.