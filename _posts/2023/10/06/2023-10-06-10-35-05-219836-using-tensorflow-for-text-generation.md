---
layout: post
title: "[python] Using TensorFlow for text generation"
description: " "
date: 2023-10-06
tags: [python]
comments: true
share: true
---

Text generation is a fascinating application of machine learning that involves generating new text based on a given input. With the help of deep learning frameworks like TensorFlow, we can train models to generate creative and human-like text.

In this blog post, we will explore how to use TensorFlow for text generation and walk through a simple example to generate text based on existing text data.

## Table of Contents
- [Introduction to Text Generation](#introduction-to-text-generation)
- [Using TensorFlow for Text Generation](#using-tensorflow-for-text-generation)
- [Example: Generating Text with TensorFlow](#example-generating-text-with-tensorflow)
- [Conclusion](#conclusion)

## Introduction to Text Generation

Text generation is the process of training a model to generate new text that is coherent and similar to the input text. It can be used for various applications like generating song lyrics, writing poetry, creating dialogues, and much more.

Deep learning models, specifically Recurrent Neural Networks (RNNs), are commonly used for text generation. RNNs are well suited for sequential data like text, as they can capture the contextual dependencies and generate text based on the patterns learned from the training data.

## Using TensorFlow for Text Generation

TensorFlow is a popular deep learning framework that provides a wide range of tools and capabilities for training and deploying machine learning models. It also offers several built-in functionalities for text generation.

To generate text using TensorFlow, we need to follow these steps:
1. **Preprocessing**: Prepare the text data by cleaning, tokenizing, and converting it into a format suitable for training.
2. **Creating the Model**: Build a deep learning model, often using RNNs or Transformer architectures, to learn from the input text data.
3. **Training the Model**: Train the model on the text data and optimize its parameters to minimize the loss.
4. **Generating Text**: Use the trained model to generate new text by providing a seed text or by sampling from the learned probability distribution.

## Example: Generating Text with TensorFlow

Let's walk through a simple example of generating text using TensorFlow. We'll generate movie titles based on a dataset of existing movie titles.

```python
import tensorflow as tf
from tensorflow import keras

# Load the movie titles dataset
data = open('movie_titles.txt', 'r').read()

# Preprocess the text data
tokenizer = keras.preprocessing.text.Tokenizer()
tokenizer.fit_on_texts([data])
total_words = len(tokenizer.word_index) + 1

# Convert text into sequences of tokens
input_sequences = []
for line in data.split('\n'):
    token_list = tokenizer.texts_to_sequences([line])[0]
    for i in range(1, len(token_list)):
        n_gram_sequence = token_list[:i+1]
        input_sequences.append(n_gram_sequence)

# Pad sequences for consistent length
max_sequence_len = max([len(x) for x in input_sequences])
input_sequences = keras.preprocessing.sequence.pad_sequences(input_sequences, maxlen=max_sequence_len, padding='pre')

# Split input and target sequences
input_sequences = np.array(input_sequences)
x_train = input_sequences[:, :-1]
y_train = input_sequences[:, -1]

# Build the model
model = keras.models.Sequential()
model.add(keras.layers.Embedding(total_words, 100, input_length=max_sequence_len-1))
model.add(keras.layers.Bidirectional(keras.layers.GRU(150, return_sequences=True)))
model.add(keras.layers.Dropout(0.2))
model.add(keras.layers.GRU(100))
model.add(keras.layers.Dense(total_words/2, activation='relu'))
model.add(keras.layers.Dense(total_words, activation='softmax'))
model.compile(loss='sparse_categorical_crossentropy', optimizer='adam', metrics=['accuracy'])

# Train the model
history = model.fit(x_train, y_train, epochs=100, verbose=1)

# Generate text
seed_text = "fantasy adventure"
next_words = 10

for _ in range(next_words):
    token_list = tokenizer.texts_to_sequences([seed_text])[0]
    token_list = keras.preprocessing.sequence.pad_sequences([token_list], maxlen=max_sequence_len-1, padding='pre')
    predicted = model.predict_classes(token_list, verbose=0)
    output_word = ""
    for word, index in tokenizer.word_index.items():
        if index == predicted:
            output_word = word
            break
    seed_text += " " + output_word

print(seed_text)
```

In this example, we start by loading the movie titles dataset and preprocessing the text data using the Tokenizer API provided by TensorFlow. We then create input sequences, pad them for consistent length, and split them into input and target sequences.

Next, we build a sequential model using a combination of embedding layers and recurrent layers (GRU). We compile and train the model using the specified loss function and optimizer. Finally, we generate new text by providing a seed text and using the trained model to predict the next word.

## Conclusion

Text generation using TensorFlow is a powerful capability that enables us to create AI-powered systems for generating new and creative text. By leveraging deep learning techniques and frameworks like TensorFlow, we can train models to generate text that closely aligns with the patterns in the training data.

Whether it's for creative writing, chatbots, or content generation, text generation with TensorFlow opens up a wide range of possibilities. Give it a try and start generating your own text-based content using deep learning!