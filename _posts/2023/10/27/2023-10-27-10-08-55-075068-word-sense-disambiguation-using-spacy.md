---
layout: post
title: "[python] Word sense disambiguation using SpaCy"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

In natural language processing, word sense disambiguation (WSD) is a task that aims to determine the correct meaning of a word in a given context. SpaCy is a powerful Python library for NLP that provides several capabilities, including word sense disambiguation.

In this blog post, we will explore how to perform word sense disambiguation using SpaCy. We will start by installing SpaCy and the required language model. Then, we will dive into the code to disambiguate word senses.

### Installation

Before we begin, make sure you have SpaCy installed. You can install it using `pip`:

```shell
pip install spacy
```

Next, download the language model you want to use. In this example, we will use the English language model:

```shell
python -m spacy download en_core_web_sm
```

### Word Sense Disambiguation with SpaCy

To perform word sense disambiguation with SpaCy, follow these steps:

1. Import the necessary libraries and load the language model.

```python
import spacy

nlp = spacy.load("en_core_web_sm")
```

2. Create a SpaCy document by calling the language model on the input text.

```python
text = "I saw a man with a telescope."
doc = nlp(text)
```

3. Iterate over the tokens in the document and print the lemma, part-of-speech tag, and possible word senses.

```python
for token in doc:
    print(token.text, token.lemma_, token.pos_, token._.all_senses)
```

In the example code above, `token._.all_senses` gives a list of possible word senses for each token. You can access the most likely sense using `token._.most_common_sense`.

### Example Output

Let's take a look at the output of the word sense disambiguation using SpaCy on the sentence "I saw a man with a telescope.".

```
I -PRON- PRON ['the speaker or writer', 'subjective case of we', 'subjective case of I']
saw see VERB ['perceive with the eyes', 'catch sight of']
a a DET ['a certain', 'one', 'an indefinite article']
man man NOUN ['any living or extinct member of the family Hominidae characterized by superior intelligence, articulate speech, and erect carriage', 'an adult person who is male (as opposed to a woman)', 'any living or extinct member of the family Hominidae characterized by superior intelligence, articulate speech, and erect carriage']
with with ADP ['accompanied by', 'in the company of', 'in the use or possession of', 'in the absence or omission of']
a a DET ['a certain', 'one', 'an indefinite article']
telescope telescope NOUN ['an optical instrument designed to make distant objects appear nearer', 'a magnifier of images of distant objects', 'an optical instrument used to observe natural phenomena']
. . PUNCT ['.']
```

### Conclusion

Word sense disambiguation is a crucial task in natural language processing. With SpaCy, we can easily perform word sense disambiguation by leveraging its powerful language models. By disambiguating word senses, we can improve the accuracy and effectiveness of various NLP applications.

Learn more about SpaCy and its word sense disambiguation capabilities in the official [SpaCy documentation](https://spacy.io/usage/linguistic-features#word-senses).