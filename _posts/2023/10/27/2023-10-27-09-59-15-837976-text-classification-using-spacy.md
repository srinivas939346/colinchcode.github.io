---
layout: post
title: "[python] Text classification using SpaCy"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

Text classification is the task of assigning predefined categories or labels to text documents based on their content. It has applications in various domains such as sentiment analysis, spam detection, and news categorization.

In this blog post, we will explore how to perform text classification using SpaCy - a popular and powerful natural language processing library in Python.

## Installing SpaCy

Before we begin, make sure you have SpaCy installed. You can install it using pip:

```
pip install spacy
```

After installing SpaCy, you'll also need to download the language model that you want to use. For example, to download the English language model, use the following command:

```
python -m spacy download en
```

## Building a Text Classification Model

To build a text classification model using SpaCy, we will follow these steps:

1. **Data Preparation**: First, we need to prepare our data. We should have a labeled dataset consisting of text documents and their corresponding categories.

2. **Feature Extraction**: SpaCy provides a powerful and efficient way to extract features from text documents using its language models. We can use the SpaCy tokenizer to tokenize our text into individual words, and then convert them into word vectors.

3. **Model Training**: After extracting the features, we can train a machine learning model to classify the text documents into different categories. SpaCy provides a simple interface to train and evaluate text classification models.

## Example: Sentiment Analysis

As an example, let's build a sentiment analysis model using SpaCy. We'll use the [IMDb movie review dataset](https://ai.stanford.edu/~amaas/data/sentiment/) which contains movie reviews labeled as positive or negative.

```python
import spacy
import random
from spacy.util import minibatch, compounding

# Load the language model
nlp = spacy.load("en")

# Prepare the training data
train_data = [
    ("This movie was great!", {"cats": {"POSITIVE": 1, "NEGATIVE": 0}}),
    ("I absolutely loved it!", {"cats": {"POSITIVE": 1, "NEGATIVE": 0}}),
    ("The acting was terrible.", {"cats": {"POSITIVE": 0, "NEGATIVE": 1}}),
    ("It was a waste of time.", {"cats": {"POSITIVE": 0, "NEGATIVE": 1}}),
]

# Train the text classification model
nlp.begin_training()
for i in range(10):
    random.shuffle(train_data)
    losses = {}
    batches = minibatch(train_data, size=8)
    for batch in batches:
        texts, annotations = zip(*batch)
        nlp.update(texts, annotations, losses=losses, drop=0.5)
    print(f"Loss: {losses['textcat']:.4f}")

# Test the model
test_data = [
    "The movie was fantastic!",
    "I didn't enjoy watching it.",
]

for text in test_data:
    doc = nlp(text)
    category = doc.cats.most_common(1)[0][0]
    print(f"Text: {text} | Category: {category}")
```

In this example, we define our training data which consists of labeled movie reviews. We train our text classification model using the `nlp.update()` method. After training, we test the model by predicting the category for some test texts.

## Conclusion

In this blog post, we learned how to perform text classification using SpaCy. SpaCy provides a convenient interface for building text classification models. You can experiment with different datasets and explore other uses cases to further enhance your understanding of text classification with SpaCy.

References:
- [SpaCy Documentation](https://spacy.io/)
- [IMDb movie review dataset](https://ai.stanford.edu/~amaas/data/sentiment/)