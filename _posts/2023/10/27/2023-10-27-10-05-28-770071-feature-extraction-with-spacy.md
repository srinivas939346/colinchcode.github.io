---
layout: post
title: "[python] Feature extraction with SpaCy"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

When working with natural language processing (NLP) tasks, it is often necessary to extract relevant features from text data. Feature extraction plays a crucial role in tasks such as text classification, named entity recognition, and sentiment analysis.

SpaCy is a popular Python library for NLP that provides efficient and accurate tokenization, part-of-speech tagging, and entity recognition capabilities. In addition to these core functionalities, SpaCy also allows us to extract custom features from text data.

In this blog post, we will explore how to perform feature extraction with SpaCy using its built-in capabilities and custom techniques.

#### Installation

Before we get started, let's make sure SpaCy is installed. You can install it using pip:

```python
pip install spacy
```

We also need to download the specific language model we want to use. For example, to use the English language model, we can run:

```python
python -m spacy download en_core_web_sm
```

#### Built-in Features

SpaCy provides several built-in features that are readily available for feature extraction. Some of the most commonly used ones include:

##### Part-of-Speech (POS) Tagging

POS tagging assigns a part-of-speech label to each word in a sentence, such as noun, verb, adjective, etc. To extract POS tags using SpaCy, we can use the `pos_` attribute of the `Token` object. Here's an example:

```python
import spacy

nlp = spacy.load('en_core_web_sm')

text = "The cat is sitting on the mat."
doc = nlp(text)

pos_tags = [token.pos_ for token in doc] # Extract POS tags

print(pos_tags)
# Output: ['DET', 'NOUN', 'AUX', 'VERB', 'ADP', 'DET', 'NOUN', '.']
```

##### Named Entity Recognition (NER)

NER aims to identify and classify named entities in text, such as persons, organizations, locations, etc. SpaCy provides an `ents` attribute that contains the named entities identified in the document. Each entity has attributes like `text`, `start`, `end`, `label`, etc. Here's an example:

```python
import spacy

nlp = spacy.load('en_core_web_sm')

text = "Apple Inc. was founded by Steve Jobs in Cupertino, California."
doc = nlp(text)

entities = [(ent.text, ent.label_) for ent in doc.ents] # Extract named entities

print(entities)
# Output: [('Apple Inc.', 'ORG'), ('Steve Jobs', 'PERSON'), ('Cupertino', 'GPE'), ('California', 'GPE')]
```

#### Custom Features

In addition to the built-in features, SpaCy allows us to extract custom features from text data. This is particularly useful when we want to capture specific patterns or linguistic information in our data. Here's an example of how to extract custom features using SpaCy:

```python
import spacy

nlp = spacy.load('en_core_web_sm')

text = "I love to eat pizza."
doc = nlp(text)

custom_features = [token.is_alpha for token in doc] # Custom feature: Is the token alphabetic?

print(custom_features)
# Output: [True, True, True, True, False]
```

In the example above, we extracted a custom feature indicating whether each token in the text is alphabetic or not.

#### Conclusion

SpaCy is a powerful library for NLP tasks, providing a wide range of features for efficient and accurate text processing. In this blog post, we explored how to perform feature extraction using SpaCy's built-in capabilities and custom techniques.

By leveraging the built-in features like POS tagging and named entity recognition, as well as creating our own custom features, we can extract valuable information from text data and improve the performance of NLP models and applications.

References:
- [SpaCy Documentation](https://spacy.io/)
- [SpaCy GitHub Repository](https://github.com/explosion/spaCy)

Now you have the tools to start extracting features from text data using SpaCy. Happy coding!