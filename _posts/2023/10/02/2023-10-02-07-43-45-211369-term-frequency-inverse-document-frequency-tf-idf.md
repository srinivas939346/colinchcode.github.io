---
layout: post
title: "[python] Term Frequency-Inverse Document Frequency (TF-IDF)"
description: " "
date: 2023-10-02
tags: [python]
comments: true
share: true
---

TF-IDF is a popular algorithm used in text mining and information retrieval to measure the importance of a term within a document or a collection of documents. It is commonly used to calculate the relevance of a keyword to a document in search engines.

## What is TF-IDF?

TF-IDF calculates a weight for each term in a document by considering two factors: term frequency (TF) and inverse document frequency (IDF).

- Term Frequency (TF) measures how often a term appears in a document. Higher TF indicates that a term is more important or relevant to the document.
- Inverse Document Frequency (IDF) measures how rare or informative a term is across all documents. The rarer the term, the higher its IDF.

The TF-IDF score for a term in a document is calculated by multiplying its TF with its IDF.

## How to calculate TF-IDF?

The TF-IDF algorithm can be implemented in several steps:

### Step 1: Preprocessing

Before calculating TF-IDF, you need to preprocess the text data. This step typically includes tokenization, removing stop words, and stemming or lemmatization to normalize the words.

### Step 2: Calculate Term Frequency (TF)

Calculate the term frequency for each term in a document. Term frequency is the count of how often a term appears in the document.

### Step 3: Calculate Inverse Document Frequency (IDF)

Calculate the inverse document frequency for each term. IDF is calculated using the formula:

```
IDF = log(total documents / number of documents containing the term)
```

### Step 4: Calculate TF-IDF score

Multiply the term frequency (TF) with the inverse document frequency (IDF) to calculate the TF-IDF score for each term in a document.

## Example

Let's consider a simple example. Suppose we have a collection of three documents:

1. Document 1: "The cat sat on the mat"
2. Document 2: "The dog chased the cat"
3. Document 3: "The mat is soft"

### Step 1: Preprocessing

After preprocessing, the documents become:

1. Document 1: ["cat", "sat", "mat"]
2. Document 2: ["dog", "chased", "cat"]
3. Document 3: ["mat", "soft"]

### Step 2: Calculate Term Frequency (TF)

For each document, calculate the term frequency:

1. Document 1: {"cat": 1, "sat": 1, "mat": 1}
2. Document 2: {"dog": 1, "chased": 1, "cat": 1}
3. Document 3: {"mat": 1, "soft": 1}

### Step 3: Calculate Inverse Document Frequency (IDF)

Using the formula, calculate the IDF for each term:

```
IDF("cat") = log(3 / 2) = 0.405
IDF("sat") = log(3 / 1) = 1.099
IDF("mat") = log(3 / 2) = 0.405
IDF("dog") = log(3 / 1) = 1.099
IDF("chased") = log(3 / 1) = 1.099
IDF("soft") = log(3 / 1) = 1.099
```

### Step 4: Calculate TF-IDF score

Multiply the term frequency (TF) with the inverse document frequency (IDF) to calculate the TF-IDF score for each term in each document:

1. Document 1: {"cat": 1 * 0.405, "sat": 1 * 1.099, "mat": 1 * 0.405}
2. Document 2: {"dog": 1 * 1.099, "chased": 1 * 1.099, "cat": 1 * 0.405}
3. Document 3: {"mat": 1 * 0.405, "soft": 1 * 1.099}

The final TF-IDF scores for each term in each document can be used to determine the importance or relevance of the terms within the documents.

## Conclusion

TF-IDF is a powerful algorithm for measuring the importance of terms within documents. It enables effective keyword extraction, information retrieval, and search engine ranking. Understanding how TF-IDF works can help you improve various NLP tasks and extract meaningful insights from textual data.