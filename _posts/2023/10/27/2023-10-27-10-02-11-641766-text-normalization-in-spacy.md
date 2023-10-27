---
layout: post
title: "[python] Text normalization in SpaCy"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

In natural language processing (NLP), text normalization is an essential step to clean and prepare text data for further analysis. Normalizing text involves transforming the text in a standardized format by removing or replacing certain characters, symbols, punctuation marks, or special characters.

SpaCy is a popular Python library for NLP tasks that provides built-in functionality for text normalization. In this blog post, we will explore how to perform text normalization using SpaCy.

### Installing SpaCy

To get started, you need to install SpaCy. You can install it using pip by running the following command:

```python
pip install spacy
```

Additionally, you will need to download the language model for the specific language you want to work with. For example, if you want to work with English text, you can download the English language model with the command:

```python
python -m spacy download en
```

### Text Normalization Techniques

SpaCy provides various techniques for text normalization, including:

1. **Tokenization**: Breaking down the text into individual words or tokens.
2. **Lemmatization**: Reducing words to their base or root form.
3. **Stop Word Removal**: Eliminating common words that do not carry much meaning, such as "the", "is", "and", etc.
4. **Lowercasing**: Converting all text to lowercase.

Let's see how we can apply these techniques using SpaCy.

### Example Code

```python
import spacy

# Load the language model
nlp = spacy.load('en')

# Define a sample text
text = "I am running late for the party! Can't wait to see everyone."

# Tokenization
doc = nlp(text)
tokens = [token.text for token in doc]
print("Tokens:", tokens)

# Lemmatization and lowercasing
normalized_text = [token.lemma_.lower() for token in doc if not token.is_punct and not token.is_stop]
print("Normalized Text:", normalized_text)
```

In the above code, we first load the English language model in SpaCy. Then, we define a sample text that needs to be normalized.

We use the `nlp` object to process the text and obtain a `doc` object. From the `doc` object, we can extract the individual tokens using a list comprehension.

Next, we perform lemmatization and lowercasing on the tokens. We exclude punctuation and stop words using conditional statements to create the `normalized_text` list.

Finally, we print the original tokens and the normalized text for comparison.

### Conclusion

Text normalization is an important step in any NLP pipeline, and SpaCy provides a convenient and efficient way to perform text normalization. In this blog post, we explored how to use SpaCy for tokenization, lemmatization, stop word removal, and lowercasing. By applying these techniques, you can ensure that your text data is in a consistent and standardized format for further analysis.

References:
- [SpaCy documentation](https://spacy.io/)
- [SpaCy GitHub repository](https://github.com/explosion/spaCy)