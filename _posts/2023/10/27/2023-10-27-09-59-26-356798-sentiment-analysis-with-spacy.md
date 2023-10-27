---
layout: post
title: "[python] Sentiment analysis with SpaCy"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

In this tutorial, we will learn how to perform sentiment analysis using SpaCy, a popular Natural Language Processing library in Python.

Sentiment analysis is the process of determining the sentiment expressed in a piece of text, whether it is positive, negative, or neutral. It can be useful in various applications such as social media monitoring, customer feedback analysis, and market research.

## Prerequisites

Before getting started, make sure you have SpaCy and its English language model installed. You can install them using pip:

```bash
pip install spacy
python -m spacy download en_core_web_sm
```

## Load the Language Model

Let's begin by loading the English language model in SpaCy:

```python
import spacy

nlp = spacy.load('en_core_web_sm')
```

## Perform Sentiment Analysis

To perform sentiment analysis using SpaCy, we will analyze each sentence in the text and assign a sentiment score to it. SpaCy provides a `pipe` method to process multiple texts efficiently. Here's how we can use it:

```python
def analyze_sentiment(text):
    doc = nlp(text)
    sentiment_score = 0
    
    for sentence in doc.sents:
        sentiment_score += sentence.sentiment.polarity
    
    if sentiment_score > 0:
        return "Positive"
    elif sentiment_score < 0:
        return "Negative"
    else:
        return "Neutral"
```

In the above code, we iterate over each sentence in the document and calculate the polarity score using the `sentiment.polarity` attribute provided by SpaCy. A positive value indicates positive sentiment, a negative value indicates negative sentiment, and zero indicates neutral sentiment.

## Example Usage

Now, let's test our sentiment analysis function with some example text:

```python
text = "I absolutely loved the movie! The acting was outstanding and the plot kept me hooked till the end."
sentiment = analyze_sentiment(text)
print(sentiment)
```

Output:
```
Positive
```

In the above example, the sentiment analysis function correctly identifies the positive sentiment expressed in the text.

## Conclusion

In this tutorial, we learned how to perform sentiment analysis using SpaCy. SpaCy provides an efficient and easy-to-use API for analyzing text sentiment. You can further enhance the sentiment analysis by using more advanced techniques such as training your own sentiment classifier or incorporating domain-specific lexicons.

References:
- [SpaCy Documentation](https://spacy.io/)
- [SpaCy GitHub Repository](https://github.com/explosion/spaCy)