---
layout: post
title: "[python] Named entity recognition (NER) using Keras"
description: " "
date: 2023-10-23
tags: [python]
comments: true
share: true
---

Named Entity Recognition (NER) is a task in Natural Language Processing (NLP) that involves identifying and classifying named entities (such as people, organizations, locations, etc.) in text. In this blog post, we'll explore how to perform NER using Keras, a popular deep learning library.

## Table of Contents
1. [Introduction](#introduction)
2. [Data Preparation](#data-preparation)
3. [Model Architecture](#model-architecture)
4. [Training the Model](#training-the-model)
5. [Evaluation and Prediction](#evaluation-and-prediction)
6. [Conclusion](#conclusion)

## Introduction <a name="introduction"></a>

NER is a fundamental task in NLP and has various applications, including information retrieval, question answering, and sentiment analysis. Deep learning models have shown promising results in NER, and Keras provides a convenient framework for building and training such models.

## Data Preparation <a name="data-preparation"></a>

To train our NER model, we need labeled data containing text along with corresponding entities. Typically, the data is in the IOB format (Inside, Outside, Beginning), where each word is labeled with a tag indicating whether it is the beginning of an entity, inside an entity, or outside an entity.

Once we have the labeled data, we can preprocess it by tokenizing the text and converting the labels into numerical representations. Keras provides useful preprocessing functions, such as `Tokenizer`, to simplify this step.

```python
# Code example for data preparation

from tensorflow.keras.preprocessing.text import Tokenizer
from tensorflow.keras.preprocessing.sequence import pad_sequences

# Tokenize the text and convert labels
tokenizer = Tokenizer()
tokenizer.fit_on_texts(texts)
word_index = tokenizer.word_index

sequences = tokenizer.texts_to_sequences(texts)
X = pad_sequences(sequences, maxlen=max_len)

# Convert labels into numerical representations
label_tokenizer = Tokenizer()
label_tokenizer.fit_on_texts(labels)
label_index = label_tokenizer.word_index

label_sequences = label_tokenizer.texts_to_sequences(labels)
y = pad_sequences(label_sequences, maxlen=max_len)
```

## Model Architecture <a name="model-architecture"></a>

For NER, a common approach is to use a BiLSTM (Bidirectional Long Short-Term Memory) model with a CRF (Conditional Random Field) layer on top. The BiLSTM layer captures contextual information from the input sequence, and the CRF layer models the dependencies between the labels.

```python
# Code example for model architecture

from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Embedding, Bidirectional, LSTM, TimeDistributed, Dense, Activation
from tensorflow.keras_contrib.layers import CRF

# Build the model architecture
model = Sequential()
model.add(Embedding(input_dim=len(word_index)+1, output_dim=embedding_dim, input_length=max_len))
model.add(Bidirectional(LSTM(units=hidden_units, return_sequences=True)))
model.add(TimeDistributed(Dense(units=len(label_index)+1)))
crf = CRF(len(label_index)+1)
model.add(crf)
model.compile(optimizer='adam', loss=crf.loss_function, metrics=[crf.accuracy])
```

## Training the Model <a name="training-the-model"></a>

To train the NER model, we can split our preprocessed data into training and validation sets. We then fit the model to the training data and monitor its performance on the validation data.

```python
# Code example for training the model

history = model.fit(X_train, y_train, validation_data=(X_val, y_val), batch_size=batch_size, epochs=num_epochs)
```

## Evaluation and Prediction <a name="evaluation-and-prediction"></a>

After training, we can evaluate the model's performance using standard metrics such as precision, recall, and F1 score. Additionally, we can use the trained model to make predictions on new, unseen data.

```python
# Code example for evaluation and prediction

# Evaluate the model
model.evaluate(X_test, y_test)

# Making predictions
predictions = model.predict(X_test)

# Convert predicted labels to text
predicted_labels = label_tokenizer.sequences_to_texts(predictions)
```

## Conclusion <a name="conclusion"></a>

In this blog post, we explored how to perform Named Entity Recognition (NER) using Keras, a popular deep learning library. We covered the data preparation steps, model architecture, training process, and evaluation/prediction. NER is an important task in NLP with various applications, and utilizing deep learning models can lead to improved performance.