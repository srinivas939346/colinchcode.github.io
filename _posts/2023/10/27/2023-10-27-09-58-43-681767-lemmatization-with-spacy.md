---
layout: post
title: "[python] Lemmatization with SpaCy"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

Lemmatization is a text normalization technique that reduces words to their base or root form. It helps in reducing the inflectional forms of words to their common base form, which makes it easier to analyze and process textual data.

In this blog post, we will explore how to perform lemmatization using SpaCy, a popular and efficient open-source natural language processing library in Python.

## Installing SpaCy

To get started, you need to install SpaCy. Open your terminal and run the following command:

```shell
pip install spacy
```

You also need to download the language model for the specific language you want to perform lemmatization on. To download the English language model, run the following command:

```shell
python -m spacy download en_core_web_sm
```

## Lemmatization in SpaCy

Now that we have installed SpaCy and downloaded the language model, let's see how to perform lemmatization using SpaCy in Python.

First, we need to load the language model using `spacy.load` and initialize it with the language model name. In this case, we will use the English language model:

```python
import spacy

nlp = spacy.load('en_core_web_sm')
```

Next, we will create a SpaCy document by passing the text to the `nlp` object:

```python
text = "I am running in the park"
doc = nlp(text)
```

Now, we can iterate over each token in the document and access its lemma using the `token.lemma_` attribute:

```python
lemmatized_text = " ".join([token.lemma_ for token in doc])
print(lemmatized_text)
```

This will produce the lemmatized version of the text: "I be run in the park".

## Conclusion

Lemmatization is an important step in preprocessing textual data before performing analysis or building natural language processing models. SpaCy provides an efficient and easy-to-use lemmatization feature, making it a great choice for text normalization tasks.

In this blog post, we learned how to perform lemmatization using SpaCy in Python. We installed SpaCy, downloaded the language model, and showcased a simple example of lemmatizing text.

References:
- [SpaCy documentation](https://spacy.io/usage/linguistic-features#lemmatizer)
- [SpaCy GitHub repository](https://github.com/explosion/spaCy)