---
layout: post
title: "[python] Document classification"
description: " "
date: 2023-10-02
tags: [python]
comments: true
share: true
---

Document classification is the process of automatically categorizing a document into predefined categories or classes based on its content. It is a common problem in natural language processing (NLP) and can be applied to a variety of tasks, such as spam detection, sentiment analysis, and topic classification.

In this tutorial, we will explore how to perform document classification using Python and a popular machine learning library called Scikit-learn.

## Table of Contents
- [Installing Scikit-learn](#installing-scikit-learn)
- [Loading the Dataset](#loading-the-dataset)
- [Text Preprocessing](#text-preprocessing)
- [Feature Extraction](#feature-extraction)
- [Model Training](#model-training)
- [Making Predictions](#making-predictions)
- [Conclusion](#conclusion)

## Installing Scikit-learn

First, make sure you have Python and pip installed on your system. You can then install Scikit-learn by running the following command in your terminal:

```python
pip install scikit-learn
```

## Loading the Dataset

For this tutorial, we will use a popular dataset called the "20 Newsgroups" dataset, which consists of approximately 18,000 newsgroup posts on 20 topics. You can easily load this dataset using Scikit-learn's built-in function:

```python
from sklearn.datasets import fetch_20newsgroups

categories = ['comp.graphics', 'sci.med', 'soc.religion.christian']
data = fetch_20newsgroups(categories=categories)
```

Here, we are selecting only three categories for simplicity, but you can choose any categories you are interested in.

## Text Preprocessing

To prepare the text data for classification, we need to perform some preprocessing steps, such as tokenization, removing stop words, and stemming. Here is an example of how you can preprocess the data using the NLTK library:

```python
import nltk
from nltk.corpus import stopwords
from nltk.stem import PorterStemmer

nltk.download('stopwords')

stop_words = set(stopwords.words('english'))
stemmer = PorterStemmer()

def preprocess(text):
    # Tokenization
    tokens = nltk.word_tokenize(text.lower())
    
    # Removing stop words
    tokens = [token for token in tokens if token not in stop_words]
    
    # Stemming
    tokens = [stemmer.stem(token) for token in tokens]
    
    return ' '.join(tokens)
```

## Feature Extraction

To train our document classification model, we need to transform the text data into numerical features that machine learning algorithms can understand. One common approach is to use the term frequency-inverse document frequency (TF-IDF) representation. Here's how you can extract TF-IDF features using Scikit-learn:

```python
from sklearn.feature_extraction.text import TfidfVectorizer

vectorizer = TfidfVectorizer()
X = vectorizer.fit_transform(data.data)
```

## Model Training

Now that we have our features ready, we can train a classifier on the dataset. In this tutorial, we will use the popular Support Vector Machine (SVM) algorithm. Scikit-learn provides an implementation of SVM that we can use:

```python
from sklearn.svm import SVC

model = SVC()
model.fit(X, data.target)
```

## Making Predictions

Once the model is trained, we can make predictions on new, unseen documents. We need to preprocess and extract features from the new document in the same way we did for the training data. Then, we can use the trained classifier to predict the category of the document:

```python
new_document = "This is a new document about computer graphics"
preprocessed_document = preprocess(new_document)
features = vectorizer.transform([preprocessed_document])
predicted_category = model.predict(features)
```

## Conclusion

In this tutorial, we learned how to perform document classification using Python and Scikit-learn. We covered the steps of loading the dataset, preprocessing the text, extracting features, training a model, and making predictions. Document classification is a powerful technique that can be applied to a wide range of NLP tasks, and Scikit-learn provides a user-friendly API for implementing it.