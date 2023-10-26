---
layout: post
title: "[python] Content-based filtering techniques"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

Content-based filtering is a recommendation technique that focuses on the attributes or features of an item to suggest similar items to users. This approach is commonly used in recommendation systems, where the system analyzes the content of items and makes suggestions based on the user's preferences or past behavior. In this blog post, we will explore some content-based filtering techniques commonly used in Python.

## 1. Vectorization of Textual Content

One of the key steps in content-based filtering is representing the textual content of items as numerical vectors. This is achieved through the process of vectorization. In Python, we can use libraries such as scikit-learn or TensorFlow to perform this task. Below is an example using scikit-learn's `TfidfVectorizer`:

```python
from sklearn.feature_extraction.text import TfidfVectorizer

# List of text documents
corpus = [
    "This is the first document.",
    "This document is the second document.",
    "And this is the third one.",
    "Is this the first document?"
]

# Create an instance of TfidfVectorizer
vectorizer = TfidfVectorizer()

# Fit the vectorizer to the corpus
X = vectorizer.fit_transform(corpus)

# Get the feature names
feature_names = vectorizer.get_feature_names()

# Print the feature names and corresponding vectors
for i in range(len(corpus)):
    print("Document {}: ".format(i))
    for j, feature in enumerate(feature_names):
        print("{}: {}".format(feature, X[i, j]))
```

This code takes a list of text documents as input and converts them into a numerical representation using the Term Frequency-Inverse Document Frequency (TF-IDF) technique. It prints the feature names and corresponding vectors for each document.

## 2. Cosine Similarity

Once we have the vector representation of the items, we can compute the similarity between items using techniques like cosine similarity. Cosine similarity measures the cosine of the angle between two vectors and gives a value between 0 and 1, where 0 represents no similarity and 1 represents perfect similarity.

In Python, we can use the `cosine_similarity` function from scikit-learn to compute the cosine similarity between two vectors. Here's an example:

```python
from sklearn.metrics.pairwise import cosine_similarity

# Compute the cosine similarity between two vectors
vector1 = [0.2, 0.4, 0.6]
vector2 = [0.3, 0.5, 0.7]

similarity = cosine_similarity([vector1], [vector2])

print("Cosine similarity:", similarity[0, 0])
```

This code calculates the cosine similarity between `vector1` and `vector2` and prints the result.

## 3. Building a Content-based Recommender

With the vectorization and similarity calculations in place, we can now build a content-based recommender system. Here's a simplified example:

```python
import numpy as np

class ContentBasedRecommender:
    def __init__(self, items, vectors):
        self.items = items
        self.vectors = vectors

    def recommend_items(self, item, num_items):
        # Get the index of the provided item
        item_index = np.where(self.items == item)[0][0]

        # Calculate the cosine similarity between the item and all other items
        similarities = cosine_similarity([self.vectors[item_index]], self.vectors)

        # Sort the similarities in descending order
        sorted_indices = np.argsort(similarities)[0][::-1]

        # Get the top recommended items
        top_items = self.items[sorted_indices[1:num_items+1]]

        return top_items

# Example usage
items = np.array(["item1", "item2", "item3", "item4"])
vectors = np.array([
    [0.2, 0.4, 0.6],
    [0.3, 0.5, 0.7],
    [0.1, 0.3, 0.9],
    [0.6, 0.2, 0.4]
])

recommender = ContentBasedRecommender(items, vectors)
recommended_items = recommender.recommend_items("item1", 2)

print("Recommended items:", recommended_items)
```

This code defines a `ContentBasedRecommender` class that takes a list of items and their corresponding vectors as input. The `recommend_items` method takes an item and the number of items to recommend as input and returns the top recommended items based on their similarity to the provided item.

## Conclusion

Content-based filtering techniques help in building recommendation systems that suggest items to users based on their characteristics or features. In this blog post, we discussed the vectorization of textual content, cosine similarity, and building a content-based recommender system using Python. These techniques can be combined with other recommendation algorithms to provide personalized recommendations to users.

References:
- [Scikit-learn TfidfVectorizer Documentation](https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.TfidfVectorizer.html)
- [Scikit-learn cosine_similarity Documentation](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.pairwise.cosine_similarity.html)