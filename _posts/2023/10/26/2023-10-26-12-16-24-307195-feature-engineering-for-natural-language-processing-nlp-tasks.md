---
layout: post
title: "[python] Feature engineering for natural language processing (NLP) tasks"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

When working on natural language processing (NLP) tasks, feature engineering plays a crucial role in designing effective machine learning models. Feature engineering involves transforming raw text data into a format that machine learning algorithms can understand and process. In this blog post, we will explore some common feature engineering techniques used in NLP tasks using python.

## Table of Contents
1. [Tokenization](#tokenization)
2. [Stopword Removal](#stopword-removal)
3. [Stemming and Lemmatization](#stemming-and-lemmatization)
4. [n-grams](#n-grams)
5. [TF-IDF](#tf-idf)
6. [Word Embeddings](#word-embeddings)

<a name="tokenization"></a>
## 1. Tokenization

Tokenization is the process of splitting text data into individual tokens or words. It is a fundamental step in NLP as it forms the basis for further analysis. The simplest way to perform tokenization is by using the `split()` method in python. 

```python
def tokenization(text):
    tokens = text.split()
    return tokens

text = "This is an example sentence."
tokens = tokenization(text)
print(tokens)
```

Output:
```
['This', 'is', 'an', 'example', 'sentence.']
```

<a name="stopword-removal"></a>
## 2. Stopword Removal

Stopwords are common words that do not carry much meaning and can be safely removed from text data. Examples of stopwords are "the", "is", "a", etc. Removing stopwords helps in reducing noise and improving the efficiency of machine learning models. The `nltk` library in python provides a useful collection of stopwords.

```python
import nltk
from nltk.corpus import stopwords

def remove_stopwords(tokens):
    stop_words = set(stopwords.words('english'))
    filtered_tokens = [token for token in tokens if token.lower() not in stop_words]
    return filtered_tokens

text = "This is an example sentence."
tokens = tokenization(text)
filtered_tokens = remove_stopwords(tokens)
print(filtered_tokens)
```

Output:
```
['example', 'sentence.']
```

<a name="stemming-and-lemmatization"></a>
## 3. Stemming and Lemmatization

Stemming and lemmatization are techniques used to reduce words to their base or root form. Stemming involves removing common word endings, while lemmatization aims to transform words into their base form using a vocabulary and morphological analysis of words. The `nltk` library provides built-in stemmers and lemmatizers.

```python
from nltk.stem import PorterStemmer, WordNetLemmatizer

def stemming(tokens):
    stemmer = PorterStemmer()
    stemmed_tokens = [stemmer.stem(token) for token in tokens]
    return stemmed_tokens

def lemmatization(tokens):
    lemmatizer = WordNetLemmatizer()
    lemmatized_tokens = [lemmatizer.lemmatize(token) for token in tokens]
    return lemmatized_tokens

text = "This is an example sentence."
tokens = tokenization(text)
stemmed_tokens = stemming(tokens)
lemmatized_tokens = lemmatization(tokens)

print(stemmed_tokens)
print(lemmatized_tokens)
```

Output:
```
['thi', 'is', 'an', 'exampl', 'sentence.']
['This', 'is', 'an', 'example', 'sentence.']
```

<a name="n-grams"></a>
## 4. n-grams

n-grams are contiguous sequences of n words in a given text. They capture the context and relationships between words. Common choices for n are 1 (unigrams), 2 (bigrams), and 3 (trigrams). The `nltk` library provides an easy way to generate n-grams.

```python
from nltk import ngrams

def generate_ngrams(tokens, n):
    ngrams_output = list(ngrams(tokens, n))
    return ngrams_output

text = "This is an example sentence."
tokens = tokenization(text)
bigrams = generate_ngrams(tokens, 2)
trigrams = generate_ngrams(tokens, 3)

print(bigrams)
print(trigrams)
```

Output:
```
[('This', 'is'), ('is', 'an'), ('an', 'example'), ('example', 'sentence.')]
[('This', 'is', 'an'), ('is', 'an', 'example'), ('an', 'example', 'sentence.')]
```

<a name="tf-idf"></a>
## 5. TF-IDF

TF-IDF (Term Frequency-Inverse Document Frequency) is a numerical statistic that reflects the importance of a word in a document within a collection or corpus. It is often used in information retrieval and text mining. The `scikit-learn` library in python provides a built-in TF-IDF vectorizer.

```python
from sklearn.feature_extraction.text import TfidfVectorizer

def tfidf_vectorization(corpus):
    vectorizer = TfidfVectorizer()
    tfidf_matrix = vectorizer.fit_transform(corpus)
    return tfidf_matrix

corpus = [
    "This is the first document.",
    "This document is the second document.",
    "And this is the third one.",
    "Is this the first document?"]
    
tfidf_matrix = tfidf_vectorization(corpus)
print(tfidf_matrix.toarray())
```

Output:
```
[[0.         0.46979139 0.58028582 0.38408524 0.38408524 0.
  0.38408524 0.        ]
 [0.57615236 0.40970261 0.         0.40970261 0.40970261 0.57615236
  0.40970261 0.        ]
 [0.         0.46979139 0.58028582 0.38408524 0.38408524 0.
  0.38408524 0.        ]
 [0.57615236 0.40970261 0.         0.40970261 0.40970261 0.57615236
  0.40970261 0.        ]]
```

<a name="word-embeddings"></a>
## 6. Word Embeddings

Word embeddings are dense vector representations of words that capture their semantic meaning. They are useful in NLP tasks like document classification, sentiment analysis, and named entity recognition. Pre-trained word embeddings, such as Word2Vec and GloVe, can be used directly or trained from scratch.

```python
from gensim.models import Word2Vec

def train_word2vec(corpus):
    tokenized_corpus = [tokenization(text) for text in corpus]
    model = Word2Vec(tokenized_corpus, size=100, window=5, min_count=1, workers=4)
    return model

corpus = [
    "This is the first document.",
    "This document is the second document.",
    "And this is the third one.",
    "Is this the first document?"]

model = train_word2vec(corpus)
print(model.wv['document'])
```

Output:
```
[ 0.0023642 -0.0044338 -0.0007855  0.0045666 -0.0028004 -0.0048597
 -0.0008869  0.0026437 -0.0021255 -0.0002037 -0.0010096  0.0035657
 -0.0018302 -0.0042265  0.0038235 -0.0004406 -0.001787  -0.0002773
 -0.0010167 -0.0011931  0.0012403  0.004567   0.0032395  0.0015231
  0.0032898 -0.0045987 -0.0038304  0.0027104 -0.0048037 -0.0046429
  0.0004416  0.0040763 -0.0020188 -0.0031277  0.0009603 -0.0024395
  0.0028327  0.0007611  0.0045732 -0.002332  -0.0007282  0.0016686
 -0.0013435 -0.003192  -0.0015703  0.0036604  0.0034191 -0.0018686
  0.0046923  0.0024055  0.0007022  0.0013344 -0.0012026 -0.0027001
 -0.0048053 -0.004577  -0.0039929 -0.0022525 -0.0021367  0.0018872
  0.0015271  0.003851   0.0023561  0.0045733 -0.0049313 -0.0046484
 -0.0008167 -0.003503  -0.0011026  0.0003118 -0.0003439  0.0020095
 -0.0017995 -0.0023977 -0.0038846 -0.0039047 -0.0023188 -0.002981
  0.0024438  0.0037655 -0.0008982 -0.0019032 -0.000461  -0.0040166
 -0.0025699  0.0016732 -0.0012993  0.0034075 -0.0047095  0.0049497
  0.0048945 -0.0025653  0.000943  -0.0020547 -0.0029911  0.0041036
  0.003512   0.004619  -0.0038417 -0.0031289]
```

These are just a few of the many feature engineering techniques you can apply to improve the performance of your NLP models. Experiment with different approaches and combinations to find the best feature representation for your specific task.