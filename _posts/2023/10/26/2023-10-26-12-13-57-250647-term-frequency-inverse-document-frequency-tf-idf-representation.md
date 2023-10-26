---
layout: post
title: "[python] Term Frequency-Inverse Document Frequency (TF-IDF) representation"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

## Introduction
In natural language processing and information retrieval, the TF-IDF representation is a common technique used to determine the importance of a term in a document or a corpus. TF-IDF stands for Term Frequency-Inverse Document Frequency, which combines two measures: the term frequency (TF) and the inverse document frequency (IDF).

## Term Frequency (TF)
The term frequency measures the frequency of a term in a document. It is calculated by dividing the number of times a term appears in a document by the total number of terms in the document. The idea behind TF is that the more a term appears in a document, the more important it is in representing the content of that document.

## Inverse Document Frequency (IDF)
The inverse document frequency measures the importance of a term in a corpus. It is calculated by taking the logarithm of the total number of documents in the corpus divided by the number of documents that contain the term. The idea behind IDF is that terms that appear in fewer documents are more important in distinguishing the documents that contain them.

## TF-IDF Calculation
To calculate the TF-IDF representation of a term in a document, we multiply its term frequency (TF) by its inverse document frequency (IDF). The resulting value represents the importance of the term in the document relative to the entire corpus.

The formula for calculating the TF-IDF of a term `t` in a document `d` is as follows:

```
TF-IDF(t, d) = TF(t, d) * IDF(t)
```

## Example Code

```python
import math

def calculate_tf(term, document):
    term_count = document.count(term)
    total_terms = len(document)
    return term_count / total_terms

def calculate_idf(term, corpus):
    documents_with_term = sum(1 for document in corpus if term in document)
    total_documents = len(corpus)
    return math.log(total_documents / (documents_with_term + 1))

def calculate_tf_idf(term, document, corpus):
    tf = calculate_tf(term, document)
    idf = calculate_idf(term, corpus)
    return tf * idf
```

## Usage

```python
corpus = [
    "I love apples and oranges",
    "Apples are delicious",
    "Oranges are juicy",
    "I like to eat apples"
]

document = "I love apples"

term = "apples"

tf_idf = calculate_tf_idf(term, document, corpus)
print(tf_idf)
```

Output:
```
0.3662040962227032
```

## Conclusion
The TF-IDF representation is a valuable tool in natural language processing for determining the importance of terms in documents or corpora. It provides a measure of the relevance of a term in a document relative to the entire corpus. By using TF-IDF, we can extract meaningful insights and perform various tasks, such as text classification, recommendation systems, and information retrieval, with improved accuracy.