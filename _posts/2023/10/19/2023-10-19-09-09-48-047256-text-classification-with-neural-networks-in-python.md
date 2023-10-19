---
layout: post
title: "[python] Text classification with neural networks in Python"
description: " "
date: 2023-10-19
tags: [python]
comments: true
share: true
---

Text classification is an important task in natural language processing (NLP). It involves categorizing text documents into predefined classes or categories. In recent years, neural networks have emerged as the go-to method for text classification due to their ability to learn complex patterns and features from text data.

In this tutorial, we will explore how to perform text classification using neural networks in Python. We will be using the popular deep learning library, Keras, which provides a high-level API for building and training neural networks.

## Table of Contents
- [Setting up the Environment](#setting-up-the-environment)
- [Preparing the Data](#preparing-the-data)
- [Building the Neural Network Model](#building-the-neural-network-model)
- [Training and Evaluating the Model](#training-and-evaluating-the-model)
- [Conclusion](#conclusion)

## Setting up the Environment

Before we start, let's make sure we have all the necessary libraries installed. We will be using the following libraries:

- Python
- Keras
- nltk (Natural Language Toolkit)
- numpy

To install these libraries, you can use pip:

```python
pip install keras nltk numpy
```

## Preparing the Data

To train our text classification model, we need a labeled dataset. In this example, we will be using the [*Reuters newswire topic classification* dataset](https://archive.ics.uci.edu/ml/datasets/reuters+newswire+topics) from the UCI Machine Learning Repository.

First, let's download and extract the dataset:

```python
import nltk

nltk.download('reuters')
```

Now, let's load the dataset and preprocess the text data:

```python
from nltk.corpus import reuters
from sklearn.model_selection import train_test_split

# Load the dataset
documents = reuters.fileids()

# Split the dataset into train and test sets
train_docs, test_docs = train_test_split(documents, test_size=0.2, random_state=42)

# Load the text and labels from the dataset
train_texts = [reuters.raw(doc_id) for doc_id in train_docs]
train_labels = [reuters.categories(doc_id)[0] for doc_id in train_docs]
test_texts = [reuters.raw(doc_id) for doc_id in test_docs]
test_labels = [reuters.categories(doc_id)[0] for doc_id in test_docs]
```

## Building the Neural Network Model

Now that we have our data ready, let's build our neural network model. We will be using a simple architecture consisting of an embedding layer, a LSTM layer, and a dense layer with softmax activation.

```python
from keras.models import Sequential
from keras.layers import Embedding, LSTM, Dense

# Constants
vocab_size = 10000
max_length = 100

# Create the model
model = Sequential()
model.add(Embedding(vocab_size, 128, input_length=max_length))
model.add(LSTM(128))
model.add(Dense(128, activation='relu'))
model.add(Dense(num_classes, activation='softmax'))

# Compile the model
model.compile(optimizer='adam', loss='sparse_categorical_crossentropy', metrics=['accuracy'])
```

## Training and Evaluating the Model

Once our model is ready, we can train it on our training data and evaluate its performance on the test data.

```python
# Constants
batch_size = 64
epochs = 10

# Train the model
model.fit(train_sequences, train_labels, batch_size=batch_size, epochs=epochs, validation_data=(test_sequences, test_labels))

# Evaluate the model
loss, accuracy = model.evaluate(test_sequences, test_labels)

print(f"Test Loss: {loss:.4f}")
print(f"Test Accuracy: {accuracy:.4f}")
```

## Conclusion

In this tutorial, we learned how to perform text classification using neural networks in Python. We built a simple neural network model using Keras and trained it on the Reuters newswire topic classification dataset. By leveraging the power of neural networks, we can achieve high accuracy in text classification tasks. Neural networks have paved the way for advancements in NLP and continue to be the state-of-the-art method for text classification.