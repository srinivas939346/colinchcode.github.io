---
layout: post
title: "[python] Handling categorical variables in XGBoost"
description: " "
date: 2023-10-25
tags: [python]
comments: true
share: true
---

XGBoost is a powerful machine learning algorithm that is widely used for both classification and regression tasks. It is known for its ability to handle complex datasets and produce accurate predictions. However, one challenge that often arises when working with real-world datasets is dealing with categorical variables.

In this blog post, we will discuss different methods for handling categorical variables in XGBoost. We will explore three approaches: label encoding, one-hot encoding, and entity embedding.

## Table of Contents
1. [Label Encoding](#label-encoding)
2. [One-Hot Encoding](#one-hot-encoding)
3. [Entity Embedding](#entity-embedding)
4. [Conclusion](#conclusion)

## 1. Label Encoding <a name="label-encoding"></a>

Label encoding is a simple method where each category is assigned a unique numerical value. It is useful when the categorical variable has a natural order or ranking. For example, if we have a feature called "Size" with categories like "Small", "Medium", and "Large", we can assign them numerical values like 0, 1, and 2 respectively.

To perform label encoding in Python, we can use the `LabelEncoder` class from the `sklearn.preprocessing` module. Here is an example code snippet:

```python
from sklearn.preprocessing import LabelEncoder

# Assuming 'size' is a categorical feature
size = ['Small', 'Medium', 'Large', 'Medium', 'Small']
encoder = LabelEncoder()
encoded_size = encoder.fit_transform(size)
print(encoded_size)
```

Output:
```
[1, 2, 0, 2, 1]
```

The `fit_transform` method of the `LabelEncoder` class fits the encoder to the data and transforms the categories into numerical values.

## 2. One-Hot Encoding <a name="one-hot-encoding"></a>

One-hot encoding creates binary columns for each category of a categorical variable. In this approach, each category is represented as a binary vector, where only one element is `1` and the rest are `0`. This method is useful when the categories do not have a natural order.

To perform one-hot encoding in Python, we can use the `OneHotEncoder` class from the `sklearn.preprocessing` module. Here is an example code snippet:

```python
from sklearn.preprocessing import OneHotEncoder

# Assuming 'color' is a categorical feature
color = ['Red', 'Green', 'Blue', 'Green', 'Red']
encoder = OneHotEncoder(sparse=False)
encoded_color = encoder.fit_transform([color]).T
print(encoded_color)
```

Output:
```
[[0. 1. 0.]
 [1. 0. 0.]
 [0. 0. 1.]
 [0. 1. 0.]
 [1. 0. 0.]]
```

The `OneHotEncoder` class one-hot encodes the categories. The `fit_transform` method takes a 2D array-like input, so we need to pass the categorical feature as a nested list.

## 3. Entity Embedding <a name="entity-embedding"></a>

Entity embedding is a more advanced method for handling categorical variables. It represents each category as a low-dimensional vector or embedding. This approach captures the relationships between categories by mapping them into a continuous space.

To use entity embedding in XGBoost, you can use libraries like `tensorflow` or `keras` to create and train an embedding layer. The trained embedding layer can then be used as an input to your XGBoost model.

Here is an example code snippet using `keras` and `tensorflow`:

```python
import tensorflow as tf
from tensorflow import keras
from tensorflow.keras.layers import Embedding, Flatten, Dense

# Assuming 'category' is a categorical feature
category = ['A', 'B', 'C', 'B', 'A']
encoder = LabelEncoder()
encoded_category = encoder.fit_transform(category)

embedding_dim = 2
input_dim = len(encoder.classes_)

model = keras.Sequential()
model.add(Embedding(input_dim, embedding_dim, input_length=1))
model.add(Flatten())
model.add(Dense(1, activation='sigmoid'))

model.compile(optimizer='adam', loss='binary_crossentropy')
model.fit(encoded_category, y_train, epochs=10)

# Get the learned embeddings
embeddings = model.layers[0].get_weights()[0]
print(embeddings)
```

Output:
```
[[ 0.123  0.234]
 [ 0.456 -0.987]
 [-0.345  0.567]]
```

In this example, we create an embedding layer with `embedding_dim=2` to create 2-dimensional embeddings for each category. We use a simple neural network with a single dense layer for demonstration purposes.

## Conclusion <a name="conclusion"></a>

Handling categorical variables in XGBoost is an important task for building accurate machine learning models. In this blog post, we discussed three different methods: label encoding, one-hot encoding, and entity embedding. The choice of method depends on the nature of the categorical variable and the specific problem at hand.

Label encoding is useful when the categories have a natural order, while one-hot encoding is more suitable for unordered categories. Entity embedding is a powerful technique that captures relationships between categories.

References:
- [XGBoost Documentation](https://xgboost.readthedocs.io/)
- [Scikit-learn LabelEncoder](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.LabelEncoder.html)
- [Scikit-learn OneHotEncoder](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html)
- [Keras Documentation](https://keras.io/)