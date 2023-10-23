---
layout: post
title: "[python] Sentiment analysis using Keras"
description: " "
date: 2023-10-23
tags: [python]
comments: true
share: true
---

Sentiment analysis is a natural language processing technique that aims to determine the sentiment or emotional tone behind a piece of text. In this blog post, we will explore how to perform sentiment analysis using the Keras library in Python.

## Table of Contents

1. [Introduction to Sentiment Analysis](#Introduction-to-Sentiment-Analysis)
2. [Data Preparation](#Data-Preparation)
3. [Building the Model](#Building-the-Model)
4. [Training and Evaluation](#Training-and-Evaluation)
5. [Conclusion](#Conclusion)

## Introduction to Sentiment Analysis

Sentiment analysis is widely used in various applications such as social media monitoring, customer feedback analysis, and market research. It involves classifying text into different sentiment categories such as positive, negative, or neutral.

## Data Preparation

To perform sentiment analysis, we need labeled text data. There are various datasets available for sentiment analysis, such as the popular IMDb movie reviews dataset. The dataset consists of movie reviews along with their associated sentiment labels (positive or negative). 

First, let's import the required libraries and load the dataset:

```python
import numpy as np
from keras.datasets import imdb

# Load the IMDb movie reviews dataset
(X_train, y_train), (X_test, y_test) = imdb.load_data()
```

Next, we will preprocess the data by performing tokenization and padding. Tokenization is the process of splitting text into individual words or tokens, while padding ensures that all input sequences have the same length. 

```python
from keras.preprocessing.sequence import pad_sequences

# Set the maximum sequence length
max_len = 100

# Pad sequences to the maximum length
X_train = pad_sequences(X_train, maxlen=max_len)
X_test = pad_sequences(X_test, maxlen=max_len)
```

## Building the Model

Now that our data is prepared, we can proceed to build the sentiment analysis model using Keras. We will use a simple model architecture consisting of an embedding layer, followed by a bidirectional LSTM layer, and finally a dense output layer. 

```python
from keras.models import Sequential
from keras.layers import Embedding, LSTM, Dense, Bidirectional

# Create the model
model = Sequential()
model.add(Embedding(input_dim=10000, output_dim=64, input_length=max_len))
model.add(Bidirectional(LSTM(units=64, dropout=0.2, recurrent_dropout=0.2)))
model.add(Dense(units=1, activation='sigmoid'))

# Compile the model
model.compile(optimizer='adam', loss='binary_crossentropy', metrics=['accuracy'])
```

## Training and Evaluation

After building the model, we can train it using the prepared data. We will train the model for a few epochs and evaluate its performance on the test set.

```python
# Train the model
model.fit(X_train, y_train, batch_size=64, epochs=5, validation_data=(X_test, y_test))

# Evaluate the model
loss, accuracy = model.evaluate(X_test, y_test)
print('Test loss:', loss)
print('Test accuracy:', accuracy)
```

## Conclusion

Sentiment analysis is a powerful technique for analyzing the sentiment expressed in text data. In this blog post, we walked through the process of performing sentiment analysis using the Keras library in Python. We covered data preparation, model building, and training/evaluation steps. By understanding sentiment analysis, you can gain valuable insights from textual data and use it for various applications.

To learn more about sentiment analysis and Keras, refer to the following resources:

- [Keras documentation](https://keras.io/)
- [Deep Learning with Python by Francois Chollet](https://www.manning.com/books/deep-learning-with-python)