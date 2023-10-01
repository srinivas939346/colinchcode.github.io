---
layout: post
title: "[python] Named Entity Recognition (NER) for specific categories (e.g., person, organization)"
description: " "
date: 2023-10-02
tags: [python]
comments: true
share: true
---

Named Entity Recognition (NER) is a natural language processing task that involves identifying and classifying named entities in text into predefined categories, such as person, organization, location, and more. In this blog post, we will focus on performing NER for specific categories using Python.

## Table of Contents

1. Introduction to Named Entity Recognition
2. NER using spaCy
3. NER for specific categories
4. Conclusion

## 1. Introduction to Named Entity Recognition

Named Entity Recognition is a subtask of information extraction that aims to locate and classify named entities in text into predefined categories. Named entities can include names of persons, organizations, locations, dates, quantities, and more.

NER involves two main steps:
- Entity identification: Identifying the presence of entities in text.
- Entity classification: Assigning a predefined category to each identified entity.

## 2. NER using spaCy

spaCy is a popular Python library for natural language processing. It provides a pre-trained model for NER that can be easily used for extracting named entities from text.

To use spaCy for NER, first, you need to install the library:

```python
pip install spacy
```

Next, download the English language model:

```python
python -m spacy download en_core_web_sm
```

Then, you can use the following code to perform NER on a given text:

```python
import spacy

nlp = spacy.load('en_core_web_sm')
text = "Apple Inc. is planning to open a new store in New York City."

doc = nlp(text)

for ent in doc.ents:
    print(ent.text, ent.label_)
```

The code above loads the pre-trained English model, processes the given text, and prints the identified entities along with their labels.

## 3. NER for specific categories

To perform NER for specific categories, we need to filter the identified entities based on their labels. In spaCy, each identified entity has a corresponding `label_` attribute that represents its category.

For example, to extract only person and organization entities from the text, you can modify the above code as follows:

```python
import spacy

nlp = spacy.load('en_core_web_sm')
text = "Apple Inc. is planning to open a new store in New York City."

doc = nlp(text)

specific_categories = ['PERSON', 'ORG']

for ent in doc.ents:
    if ent.label_ in specific_categories:
        print(ent.text, ent.label_)
```

In the code snippet above, the `specific_categories` list contains the desired categories ('PERSON' and 'ORG'). Only the entities with labels matching the categories in the list will be printed.

## 4. Conclusion

Performing Named Entity Recognition (NER) for specific categories can be useful in various applications, such as extracting specific types of information from text data. In this blog post, we explored how to perform NER using spaCy and filter entities based on their categories.

By leveraging NER, you can gain valuable insights and extract structured information from unstructured text data, enabling a wide range of applications in natural language processing and information extraction.