---
layout: post
title: "[python] Named Entity Recognition (NER) using TensorFlow"
description: " "
date: 2023-10-06
tags: [python]
comments: true
share: true
---

Named Entity Recognition (NER) is a NLP (Natural Language Processing) task that involves identifying and classifying named entities in text into predefined categories such as person names, organizations, locations, medical codes, time expressions, quantities, monetary values, and percentages.

In this blog post, we will explore how to perform Named Entity Recognition using TensorFlow, an open-source machine learning framework. TensorFlow provides powerful tools for building and training neural networks, which we will leverage for this NER task.

## Getting Started

To get started, we need to install TensorFlow and its dependencies. You can install TensorFlow using pip:

```shell
pip install tensorflow
```

Next, let's import the necessary libraries and load the dataset we will be using:

```python
import tensorflow as tf

# Load the dataset
# ...
```

## Preprocessing the Data

Before training our NER model, we need to preprocess the data. This typically involves tokenizing the text into individual words and assigning labels to each word representing the named entity category.

We can use the `tokenizer` and `label_encoder` functions provided by TensorFlow to perform this preprocessing:

```python
tokenizer = tf.keras.preprocessing.text.Tokenizer()
tokenizer.fit_on_texts(sentences)

encoded_sentences = tokenizer.texts_to_sequences(sentences)
padded_sentences = tf.keras.preprocessing.sequence.pad_sequences(encoded_sentences)

label_encoder = tf.keras.preprocessing.LabelEncoder()
label_encoder.fit(labels)

encoded_labels = label_encoder.transform(labels)
```

## Building the Model

Now, let's build our NER model using TensorFlow. We will use a simple LSTM (Long Short-Term Memory) network as our base model:

```python
model = tf.keras.Sequential([
    tf.keras.layers.Embedding(input_dim=vocab_size, output_dim=embedding_dim, input_length=max_length),
    tf.keras.layers.Bidirectional(tf.keras.layers.LSTM(units=hidden_units)),
    tf.keras.layers.Dense(units=num_classes, activation="softmax")
])
```

## Training the Model

To train our model, we need to compile it with an appropriate loss function, optimizer, and metrics:

```python
model.compile(loss="sparse_categorical_crossentropy", optimizer="adam", metrics=["accuracy"])

model.fit(padded_sentences, encoded_labels, epochs=num_epochs, validation_split=0.2)
```

## Evaluating the Model

Once the model is trained, we can evaluate its performance using the test data:

```python
loss, accuracy = model.evaluate(test_sentences, test_labels)

print("Test Loss: ", loss)
print("Test Accuracy: ", accuracy)
```

## Conclusion

In this blog post, we have learned how to perform Named Entity Recognition using TensorFlow. By preprocessing the data, building the model, and training it, we can accurately classify named entities in text. TensorFlow provides a flexible and powerful framework for NLP tasks, making it a great choice for NER and other text classification tasks.

Remember to try out different architectures, hyperparameters, and techniques to improve the performance of your NER model. Happy training!