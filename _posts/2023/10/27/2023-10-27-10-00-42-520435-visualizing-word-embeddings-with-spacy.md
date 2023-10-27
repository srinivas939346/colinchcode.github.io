---
layout: post
title: "[python] Visualizing word embeddings with SpaCy"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

Word embeddings are dense vector representations of words that capture semantic and syntactic information. They have become a popular tool in natural language processing (NLP) for a variety of tasks such as text classification, entity recognition, and machine translation.

SpaCy is a powerful Python library for NLP that provides pre-trained word embeddings for different languages. In this blog post, we will explore how to visualize word embeddings with SpaCy using t-SNE, a popular dimensionality reduction technique.

## What is t-SNE?

t-SNE (t-Distributed Stochastic Neighbor Embedding) is a technique for visualizing high-dimensional data by reducing it to two or three dimensions while preserving the structure and relationships between the data points as much as possible. It is particularly useful for visualizing word embeddings because it can reveal clusters and patterns in the data.

## Preparing the data

Before we can visualize word embeddings with SpaCy and t-SNE, we need to load the pre-trained word embeddings from SpaCy. Let's start by installing SpaCy and downloading the word embeddings for the English language.

```python
!pip install spacy
!python -m spacy download en_core_web_md
```
Now, we can load the pre-trained word embeddings and create a list of words to visualize.

```python
import spacy

# Load pre-trained word embeddings
nlp = spacy.load('en_core_web_md')

# Create a list of words
words = ['cat', 'dog', 'horse', 'apple', 'orange', 'banana']
```

## Computing word embeddings

Next, we need to compute the word embeddings for the list of words using the `vector` attribute of SpaCy tokens.

```python
# Initialize an empty list to store the word embeddings
embeddings = []

# Compute word embeddings for each word
for word in words:
    token = nlp(word)[0]  # Get the first token
    embedding = token.vector  # Get the word embedding
    embeddings.append(embedding)
```

## Visualizing word embeddings

With the word embeddings computed, we can now visualize them using t-SNE. We will use the `scikit-learn` library to perform the dimensionality reduction and matplotlib for plotting.

```python
from sklearn.manifold import TSNE
import matplotlib.pyplot as plt

# Perform t-SNE dimensionality reduction
tsne = TSNE(n_components=2, random_state=42)
embeddings_tsne = tsne.fit_transform(embeddings)

# Plot the word embeddings
plt.scatter(embeddings_tsne[:, 0], embeddings_tsne[:, 1])

# Label the points with the corresponding words
for i, word in enumerate(words):
    plt.annotate(word, (embeddings_tsne[i, 0], embeddings_tsne[i, 1]))

# Show the plot
plt.show()
```

## Conclusion

In this blog post, we have seen how to visualize word embeddings with SpaCy and t-SNE. Visualizing word embeddings can provide insights into the semantic relationships and clusters within a text corpus. By using SpaCy's pre-trained word embeddings and t-SNE, we can easily visualize and interpret the word embeddings.

References:
- [SpaCy](https://spacy.io/)
- [t-SNE](https://en.wikipedia.org/wiki/T-distributed_stochastic_neighbor_embedding)
- [scikit-learn](https://scikit-learn.org/)