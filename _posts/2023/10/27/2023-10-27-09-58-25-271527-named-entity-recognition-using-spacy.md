---
layout: post
title: "[python] Named Entity Recognition using SpaCy"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

Named Entity Recognition (NER) is a task in Natural Language Processing (NLP) that involves identifying and classifying named entities in text into predefined categories such as person names, organization names, locations, dates, etc. SpaCy is a popular Python library for NLP that provides pre-trained models for performing NER.

In this blog post, we will explore how to use SpaCy for Named Entity Recognition in Python.

## Installation

To get started, you will need to install SpaCy and download the English language model.

```python
pip install spacy
python -m spacy download en
```

## Usage

Once you have SpaCy installed, you can load the English language model and use it for NER.

```python
import spacy

nlp = spacy.load("en_core_web_sm")

text = "Apple Inc. was founded by Steve Jobs, Steve Wozniak, and Ronald Wayne."
doc = nlp(text)

for entity in doc.ents:
    print(entity.text, entity.label_)
```

In the above code, we first import the `spacy` library and load the English language model. We then define a sample text and create a `Doc` object by passing the text to the `nlp` object. The `Doc` object contains the parsed text with various linguistic annotations, including named entities.

We can iterate over the `ents` property of the `Doc` object to access each named entity and its label. In this example, we print the text and label of each entity.

## Output

Running the above code will produce the following output:

```
Apple Inc. ORG
Steve Jobs PERSON
Steve Wozniak PERSON
Ronald Wayne PERSON
```

We can see that SpaCy correctly identifies "Apple Inc." as an organization and "Steve Jobs," "Steve Wozniak," and "Ronald Wayne" as persons.

## Conclusion

SpaCy provides a simple and efficient way to perform Named Entity Recognition in Python. With its pre-trained models and easy-to-use API, it allows us to extract meaningful information from text by identifying and categorizing named entities.

By combining SpaCy with other NLP techniques, we can build powerful applications such as sentiment analysis, document classification, and information extraction.