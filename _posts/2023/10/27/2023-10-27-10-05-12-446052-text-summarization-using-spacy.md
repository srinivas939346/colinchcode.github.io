---
layout: post
title: "[python] Text summarization using SpaCy"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

Text summarization is the process of generating a concise summary of a given text, while retaining its most important information. In this blog post, we will explore how to implement text summarization using SpaCy, a popular Python library for natural language processing.

## Why use SpaCy for Text Summarization?

SpaCy is a powerful and efficient library that provides various features for natural language processing tasks. It offers pre-trained language models, efficient tokenization, and syntactic parsing, making it well-suited for text summarization.

## Installation

To get started, you need to have SpaCy installed. You can easily install it using pip:

```
pip install spacy
```

You also need to download the English language model for SpaCy:

```
python -m spacy download en_core_web_sm
```

## Text Preprocessing

Before we can summarize a text, we need to preprocess it. This involves removing any unnecessary characters or stopwords that do not contribute to the meaning of the text. We can achieve this with the help of SpaCy.

```python
import spacy

nlp = spacy.load("en_core_web_sm")

def preprocess_text(text):
    doc = nlp(text)
    tokens = [token.text for token in doc if not token.is_stop and not token.is_punct]
    return " ".join(tokens)
```

In the code above, we load the English language model, `en_core_web_sm`, and define a function `preprocess_text()` that takes in the raw text and returns the preprocessed version.

## Text Summarization

Now that we have preprocessed our text, we can move on to the actual text summarization. SpaCy makes it easy to extract the most important sentences from a given text.

```python
def summarize_text(text, num_sentences=3):
    doc = nlp(text)
    sentences = [sent.text for sent in doc.sents]
    sentence_scores = {}
    
    for sentence in sentences:
        sentence_doc = nlp(sentence)
        sentence_scores[sentence] = sentence_doc._.trf_sum_score
        
    top_sentences = sorted(sentence_scores, key=sentence_scores.get, reverse=True)[:num_sentences]
    summary = " ".join(top_sentences)
    
    return summary
```

In the code above, we define a function `summarize_text()` that takes in the preprocessed text and an optional `num_sentences` parameter (default is 3, but you can adjust it as per your preference). It uses the Transformer-based sentence embeddings (`_.trf_sum_score`) provided by SpaCy to calculate the importance score for each sentence. The function then sorts the sentences based on their importance scores and selects the top `num_sentences` sentences to create the summary.

## Putting it all Together

Let's see our text summarization in action:

```python
raw_text = "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed non risus. \
Suspendisse lectus tortor, dignissim sit amet, adipiscing nec, ultricies sed, dolor. \
Cras elementum ultrices diam. Maecenas ligula massa, varius a, semper congue, euismod \
non, mi. Proin porttitor, orci nec nonummy molestie, enim est eleifend mi, non fermentum \
diam nisl sit amet erat. Duis semper. Duis arcu massa, scelerisque vitae, consequat in, \
pretium a, enim. Pellentesque congue. Ut in risus volutpat libero pharetra tempor. \
Cras vestibulum bibendum augue. Praesent egestas leo in pede."
    
preprocessed_text = preprocess_text(raw_text)
summary = summarize_text(preprocessed_text)

print("Summary:")
print(summary)
```

Running the above code will output the summarized version of the input text.

## Conclusion

In this blog post, we learned how to implement text summarization using SpaCy. SpaCy provides a convenient way to preprocess the text and extract important sentences for generating a summary. By leveraging its powerful features, you can easily incorporate text summarization into your applications or projects.

## References

- SpaCy documentation: https://spacy.io/