---
layout: post
title: "[python] Named Entity Recognition evaluation metrics in SpaCy"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

SpaCy is a popular Python library used for Natural Language Processing (NLP) tasks. One of its key features is Named Entity Recognition (NER), which is the task of identifying and classifying entities in text into predefined categories such as person names, organizations, locations, etc.

When building an NER model using SpaCy, it is essential to evaluate its performance using appropriate metrics. In this blog post, we will explore the evaluation metrics available in SpaCy for evaluating NER models.

### Precision, Recall, and F1 Score

The most commonly used evaluation metrics for NER models are precision, recall, and F1 score. SpaCy provides a convenient way to calculate these metrics using its `scorer` module.

Precision measures the percentage of correctly predicted entities out of the total predicted entities. It represents the model's ability to avoid false positives.

Recall, on the other hand, measures the percentage of correctly predicted entities out of the total true entities. It represents the model's ability to avoid false negatives.

F1 score is the harmonic mean of precision and recall and provides a single metric to evaluate the overall performance of the NER model.

Here's an example of how to calculate precision, recall, and F1 score using SpaCy:

```python
import spacy

nlp = spacy.load("en_core_web_sm")

def evaluate_ner_model(nlp, texts, labels):
    tp, fp, tn, fn = 0, 0, 0, 0
    for text, true_label in zip(texts, labels):
        doc = nlp(text)
        predicted_labels = [ent.label_ for ent in doc.ents]
        for pred_label in predicted_labels:
            if pred_label in true_label:
                tp += 1
            else:
                fp += 1
        for true_entity in true_label:
            if true_entity not in predicted_labels:
                fn += 1
                
    precision = tp / (tp + fp)
    recall = tp / (tp + fn)
    f1_score = 2 * ((precision * recall) / (precision + recall))
    
    return precision, recall, f1_score
    
texts = ["Apple Inc. is considering a new office in London.", "John Smith is a software engineer at Google."]
labels = [["ORG"], ["PERSON"]]

precision, recall, f1_score = evaluate_ner_model(nlp, texts, labels)
print(f"Precision: {precision:.2f}")
print(f"Recall: {recall:.2f}")
print(f"F1 Score: {f1_score:.2f}")
```

### Conclusion

SpaCy provides an easy way to evaluate NER models using standard metrics like precision, recall, and F1 score. By understanding these evaluation metrics, you can assess the performance of your NER models and make necessary improvements. It is important to note that evaluation metrics should not be the sole basis for model selection. It is always recommended to consider other factors such as contextual relevance and domain-specific requirements.