---
layout: post
title: "[python] Named Entity Recognition (NER)"
description: " "
date: 2023-10-02
tags: [python]
comments: true
share: true
---

Named Entity Recognition (NER) is a subtask of Natural Language Processing (NLP) that focuses on extracting and classifying named entities in text. Named entities are real-world objects such as persons, organizations, locations, dates, and more. NER is widely used in various applications like information retrieval, question answering, sentiment analysis, and machine translation.

In this blog post, we will explore how to perform Named Entity Recognition using Python and the popular NLP library, spaCy.

## Table of Contents
1. [Introduction to spaCy](#introduction-to-spacy)
2. [Installing spaCy](#installing-spacy)
3. [Loading spaCy's Pretrained Models](#loading-pretrained-models)
4. [Performing Named Entity Recognition](#performing-ner)
5. [Conclusion](#conclusion)

## 1. Introduction to spaCy <a name="introduction-to-spacy"></a>

spaCy is an open-source library for advanced Natural Language Processing tasks. It provides a simple and efficient way to process large amounts of text data. spaCy supports multiple languages and offers various features like tokenization, part-of-speech tagging, syntactic parsing, and named entity recognition.

## 2. Installing spaCy <a name="installing-spacy"></a>

You can install spaCy using pip, the Python package manager. Open your command prompt or terminal and run the following command:

```
pip install spacy
```

Additionally, you will need to download a language model for spaCy. For example, to download the English language model, run the following command:

```
python -m spacy download en
```

## 3. Loading spaCy's Pretrained Models <a name="loading-pretrained-models"></a>

Once spaCy is installed, you can load its pretrained models for different languages. To load the English language model, you can use the following code:

```python
import spacy

nlp = spacy.load('en_core_web_sm')
```

## 4. Performing Named Entity Recognition <a name="performing-ner"></a>

To perform NER using spaCy, you need to pass the text to the loaded language model. spaCy will then analyze the text and label named entities.

```python
import spacy

nlp = spacy.load('en_core_web_sm')

text = "Apple Inc. is a technology company based in California."

# Apply NER on the text
doc = nlp(text)

# Iterate over the extracted named entities
for ent in doc.ents:
    print(ent.text, ent.label_)
```

The code above will output the named entities along with their corresponding labels:

```
Apple Inc. ORG
California GPE
```

## 5. Conclusion <a name="conclusion"></a>

Named Entity Recognition is a crucial component in many NLP applications. With libraries like spaCy, performing NER becomes easier and more accessible. Python, with its vast ecosystem of libraries, provides a powerful platform for NER and other NLP tasks.

In this blog post, we explored how to perform Named Entity Recognition using spaCy in Python. We covered the installation process, loading pretrained models, and extracting named entities from text.