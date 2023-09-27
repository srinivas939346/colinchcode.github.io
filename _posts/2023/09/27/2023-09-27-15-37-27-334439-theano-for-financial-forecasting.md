---
layout: post
title: "[python] Theano for financial forecasting"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---

Financial forecasting is a crucial task in the world of finance. It involves predicting future prices or returns of financial instruments such as stocks, commodities, or currencies. Accurate forecasting helps investors and traders make informed decisions and mitigate risks.

In this blog post, we will explore how **Theano**, a popular Python library, can be used for financial forecasting tasks. **Theano** is a numerical computation library that allows you to define, optimize, and evaluate mathematical expressions involving multi-dimensional arrays efficiently. It provides a high-level, flexible interface for writing efficient and optimized mathematical operations.

## What is Theano?

**Theano** is an open-source library developed by the Montreal Institute for Learning Algorithms (MILA) at the University of Montreal. It is widely used in various research and industry applications due to its ability to efficiently perform computations on both CPUs and GPUs.

The main strength of **Theano** lies in defining mathematical expressions using symbolic variables and applying optimizations to these expressions for efficient computation. It automatically optimizes the computation graph and generates efficient C or CUDA code, making it well-suited for tasks that involve large-scale computations.

## Using Theano for Financial Forecasting

To demonstrate the usage of **Theano** for financial forecasting, let's consider an example of predicting stock prices. We will use historical stock price data to train a model and forecast the future prices.

### Data Preparation

First, we need to gather historical stock price data. There are various ways to obtain this data, such as using APIs provided by financial data vendors or web scraping techniques. Once we have the data, we can preprocess and transform it as per our requirements.

For the purpose of this example, let's assume we have obtained the historical stock price data for a particular stock and it is already preprocessed and ready for further analysis.

### Building the Forecasting Model

Next, we will build a forecasting model using **Theano**. In this example, we will use a simple feedforward neural network as our model. The neural network will take past stock prices as input and predict the future stock prices.

Let's consider the following code snippet that demonstrates how to define a neural network model using **Theano**:

```python
import theano
import theano.tensor as T

# Define the symbolic variables for input and output
X = T.matrix('X')  # Input matrix with past stock prices
y = T.vector('y')  # Output vector with future stock prices

# Define the parameters of the neural network
W = theano.shared(value=0.01)  # Weight parameter

# Define the mathematical expression for the neural network
prediction = T.dot(X, W)  # Perform matrix multiplication

# Define the loss function
loss = T.mean(T.abs_(y - prediction))

# Define the update rule for training
learning_rate = 0.01
updates = [(W, W - learning_rate * T.grad(loss, W))]

# Compile the function for training
train = theano.function(inputs=[X, y], outputs=loss, updates=updates)
```

In this code snippet, we first define the symbolic variables `X` and `y` for the input and output of the neural network, respectively. We then define the weight parameter `W` as a shared variable.

Next, we define the mathematical expression for the neural network prediction by performing matrix multiplication of `X` and `W`. We also define the loss function, which measures the difference between the predicted stock prices and the actual stock prices.

We then define the update rule for training the neural network. We specify the learning rate and compute the gradient of the loss with respect to `W`. We update the value of `W` using the computed gradient.

Finally, we compile the function `train` that takes the input matrix `X` and the output vector `y` and performs the training using the defined update rule.

### Training and Forecasting

Once we have defined the forecasting model, we can train it on the historical stock price data. We will split the data into training and testing datasets, where we use the training data to optimize the model and the testing data to evaluate its performance.

Let's consider the following code snippet that demonstrates how to train and forecast using the defined model:

```python
import numpy as np

# Prepare the training and testing data
train_X = np.array(...)  # Input matrix with historical stock prices for training
train_y = np.array(...)  # Output vector with future stock prices for training
test_X = np.array(...)  # Input matrix with historical stock prices for testing
test_y = np.array(...)  # Output vector with future stock prices for testing

# Train the model
num_epochs = 100
for epoch in range(num_epochs):
    train_loss = train(train_X, train_y)
    print(f"Epoch {epoch+1}/{num_epochs}: Training Loss = {train_loss}")

# Forecast using the trained model
forecast = theano.function(inputs=[X], outputs=prediction)
test_predictions = forecast(test_X)
```

In this code snippet, we first prepare the training and testing data, where `train_X` and `train_y` represent the input matrix and output vector with historical stock prices for training, respectively. Similarly, `test_X` and `test_y` represent the input matrix and output vector with historical stock prices for testing, respectively.

We then iterate over multiple epochs and train the model using the `train` function. After each epoch, we print the training loss for monitoring purposes.

Finally, we use the trained model to forecast the future stock prices by calling the `forecast` function with the testing input matrix `test_X`. The forecasted stock prices are stored in the variable `test_predictions`.

### Evaluating the Forecast

Once we have the forecasted stock prices, we can evaluate the performance of our model using various metrics such as mean absolute error (MAE), root mean square error (RMSE), or R-squared.

Let's consider the following code snippet that demonstrates how to evaluate the forecasted results:

```python
from sklearn.metrics import mean_absolute_error, mean_squared_error, r2_score

# Evaluate the forecasted results
mae = mean_absolute_error(test_y, test_predictions)
rmse = mean_squared_error(test_y, test_predictions, squared=False)
r2 = r2_score(test_y, test_predictions)

print(f"MAE: {mae}, RMSE: {rmse}, R^2: {r2}")
```

In this code snippet, we import the relevant metrics functions from the `sklearn.metrics` module. We then calculate the mean absolute error (MAE), root mean square error (RMSE), and the R-squared value using the forecasted stock prices `test_predictions` and the actual stock prices `test_y`.

Finally, we print the calculated metrics to evaluate the performance of our forecasting model.

## Conclusion

In this blog post, we explored how **Theano** can be used for financial forecasting tasks. We learned about the features and advantages of **Theano**, and we demonstrated how to build a simple neural network model for predicting stock prices. We also discussed the steps for training the model, making forecasts, and evaluating the performance of the forecasted results.

Using **Theano** for financial forecasting allows us to leverage efficient computation, automatic optimization, and the flexibility of symbolic mathematical expressions. It provides a powerful tool for tackling complex financial forecasting tasks and generating accurate predictions.

Remember to experiment, fine-tune the model, and explore different architectures and techniques to improve the accuracy of your financial forecasts. Happy forecasting!