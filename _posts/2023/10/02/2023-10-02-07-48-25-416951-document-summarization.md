---
layout: post
title: "[python] Document summarization"
description: " "
date: 2023-10-02
tags: [python]
comments: true
share: true
---

In today's digital age, we are constantly bombarded with an overwhelming amount of information. Whether it is news articles, research papers, or even blog posts, it can become quite laborious to sift through all this content to find the key takeaways.

This is where document summarization comes in. Document summarization is the process of condensing long texts into shorter, more concise versions, while preserving the main ideas and important details. It can be a valuable tool for information extraction, enabling readers to quickly grasp the essence of a document without having to go through the entire text.

## TextRank Algorithm

One popular algorithm used for document summarization is the TextRank algorithm. Inspired by the PageRank algorithm used by Google, TextRank applies the concept of graph-based ranking to identify the most important sentences in a document.

To use TextRank for document summarization in Python, we can leverage the power of the Natural Language Toolkit (NLTK) library. Let's take a look at a simple implementation:

```python
import nltk
from nltk.tokenize import sent_tokenize
from nltk.corpus import stopwords
from nltk.cluster.util import cosine_distance
import numpy as np

def sentence_similarity(sent1, sent2, stopwords=None):
    if stopwords is None:
        stopwords = []
        
    words1 = nltk.word_tokenize(sent1.lower())
    words2 = nltk.word_tokenize(sent2.lower())
    
    words1 = [word for word in words1 if word.isalnum() and word not in stopwords]
    words2 = [word for word in words2 if word.isalnum() and word not in stopwords]
    
    all_words = list(set(words1 + words2))
    
    vector1 = [0] * len(all_words)
    vector2 = [0] * len(all_words)
    
    for word in words1:
        vector1[all_words.index(word)] += 1
    
    for word in words2:
        vector2[all_words.index(word)] += 1
    
    return 1 - cosine_distance(vector1, vector2)

def build_similarity_matrix(sentences, stopwords):
    similarity_matrix = np.zeros((len(sentences), len(sentences)))
    
    for i in range(len(sentences)):
        for j in range(len(sentences)):
            if i != j:
                similarity_matrix[i][j] = sentence_similarity(sentences[i], sentences[j], stopwords)
    
    return similarity_matrix

def generate_summary(text, num_sentences=3):
    sentences = sent_tokenize(text)
    stopwords = stopwords.words('english')
    
    sentence_similarity_matrix = build_similarity_matrix(sentences, stopwords)
    scores = np.array(sentence_similarity_matrix).sum(axis=1)
    ranked_sentences = [sentence for _, sentence in sorted(zip(scores, sentences), reverse=True)]
    
    return " ".join(ranked_sentences[:num_sentences])

# Usage example
document = "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Maecenas posuere arcu risus, sed dapibus augue porttitor id. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia curae; Sed condimentum, mauris eget hendrerit bibendum, sapien felis pulvinar metus, nec finibus nisi nisi ac lectus. Quisque nec urna sodales velit iaculis lobortis. Nullam accumsan eros ut metus tristique consectetur. Duis posuere risus id elit scelerisque, at feugiat orci aliquet. Suspendisse id accumsan velit. Suspendisse potenti. Nam vulputate libero metus, vitae varius leo dapibus vel. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Phasellus mattis quam sit amet sodales consequat. Nam quis lobortis dolor, eu accumsan enim. Aliquam erat volutpat."

summary = generate_summary(document)
print(summary)
```

In this example, we define three main functions: `sentence_similarity`, `build_similarity_matrix`, and `generate_summary`. The `sentence_similarity` function calculates the similarity between two sentences using cosine distance. The `build_similarity_matrix` function builds a matrix of sentence similarities. Finally, the `generate_summary` function generates the summary by ranking the sentences based on their similarity scores.

By running the code above, you would obtain a summary of the input document. Feel free to tweak the `num_sentences` parameter to generate longer or shorter summaries.

## Conclusion

Document summarization using Python can be highly beneficial for quickly extracting the key points from lengthy texts. By implementing algorithms like TextRank, we can simplify the process and make information consumption more efficient.

Keep in mind that this example serves as a starting point, and you can further enhance the summarization process by exploring other techniques and libraries. With the right tools and techniques, you can gain valuable insights from vast amounts of textual information in a matter of seconds.