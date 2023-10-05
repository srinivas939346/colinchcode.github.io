---
layout: post
title: "[python] Active learning strategies for imbalanced datasets in Python"
description: " "
date: 2023-10-05
tags: [python]
comments: true
share: true
---

In machine learning, imbalanced datasets refer to datasets where the distribution of classes is skewed, with one class having significantly more samples than the other(s). Handling imbalanced datasets poses a challenge as traditional machine learning algorithms may not perform well due to the bias towards the majority class.

Active learning is a strategy that can be employed to address imbalanced datasets. It involves iteratively selecting and annotating a subset of samples from the unlabeled dataset for model training, with the goal of improving the model's performance on the minority class.

In this blog post, we will explore some popular active learning strategies for imbalanced datasets and discuss how to implement them in Python.

## Table of Contents
1. [What is Active Learning?](#what-is-active-learning)
2. [Active Learning Strategies for Imbalanced Datasets](#active-learning-strategies)
   - [Uncertainty Sampling](#uncertainty-sampling)
   - [Query by Committee](#query-by-committee)
   - [Density Sampling](#density-sampling)
3. [Implementing Active Learning in Python](#implementing-active-learning)
4. [Conclusion](#conclusion)

## What is Active Learning? {#what-is-active-learning}

Active learning is a machine learning approach where the model is allowed to interactively query an oracle (usually a human expert) to obtain the labels for a subset of unlabeled instances. By selecting the most informative instances to label, active learning aims to achieve higher classification accuracy with fewer labeled instances.

## Active Learning Strategies for Imbalanced Datasets {#active-learning-strategies}

### Uncertainty Sampling {#uncertainty-sampling}

Uncertainty sampling is a commonly used active learning strategy for imbalanced datasets. It involves selecting instances where the model is uncertain about their class label. This can be measured using uncertainty measures such as entropy or margin of the predicted class probabilities.

```python
# Example code for uncertainty sampling
import numpy as np

# Calculate entropy of class probabilities
def entropy(probabilities):
    return -np.sum(probabilities * np.log2(probabilities))

# Calculate margin of class probabilities
def margin(probabilities):
    sorted_probs = np.sort(probabilities)
    return sorted_probs[-1] - sorted_probs[-2]

# Select instances with highest uncertainty (entropy)
def uncertainty_sampling(model, unlabeled_data, n_samples):
    uncertainties = []
    for instance in unlabeled_data:
        probabilities = model.predict_proba(instance)
        uncertainties.append(entropy(probabilities))
    uncertainties = np.array(uncertainties)
    
    selected_indices = uncertainties.argsort()[-n_samples:][::-1]
    selected_instances = unlabeled_data[selected_indices]
    
    return selected_instances
```

### Query by Committee {#query-by-committee}

Query by Committee is another active learning strategy that involves training an ensemble of models (committee), each with a different initialization or set of hyperparameters. The committee members vote on the label of each instance, with disagreement indicating uncertainty. Instances with the highest disagreement among committee members are selected for labeling.

```python
# Example code for query by committee
from sklearn.ensemble import RandomForestClassifier

# Train committee models
def train_committee_models(X_labeled, y_labeled, n_models):
    committee_models = []
    for _ in range(n_models):
        model = RandomForestClassifier()
        model.fit(X_labeled, y_labeled)
        committee_models.append(model)
    return committee_models

# Select instances with the highest disagreement among committee members
def query_by_committee(committee_models, unlabeled_data, n_samples):
    disagreement = []
    for instance in unlabeled_data:
        votes = [model.predict(instance) for model in committee_models]
        disagreement.append(np.std(votes))
    disagreement = np.array(disagreement)
    
    selected_indices = disagreement.argsort()[-n_samples:][::-1]
    selected_instances = unlabeled_data[selected_indices]
    
    return selected_instances
```

### Density Sampling {#density-sampling}

Density sampling is an active learning strategy that selects instances in regions of lower density, assuming that the minority class samples might be clustered in these regions. It utilizes density estimation techniques such as Kernel Density Estimation (KDE) or Local Outlier Factor (LOF) to determine the density of instances.

```python
# Example code for density sampling using KDE
from sklearn.neighbors import KernelDensity

# Estimate density of instances
def estimate_density(instances):
    kde = KernelDensity()
    kde.fit(instances)
    return np.exp(kde.score_samples(instances))

# Select instances with lowest density
def density_sampling(instances, n_samples):
    densities = estimate_density(instances)
    
    selected_indices = densities.argsort()[:n_samples]
    selected_instances = instances[selected_indices]
    
    return selected_instances
```

## Implementing Active Learning in Python {#implementing-active-learning}

To implement active learning strategies in Python, you can utilize popular machine learning libraries such as scikit-learn and TensorFlow. The provided example code demonstrates how to implement uncertainty sampling, query by committee, and density sampling.

## Conclusion {#conclusion}

Imbalanced datasets present challenges for machine learning, but active learning strategies offer a potential solution. Using active learning algorithms such as uncertainty sampling, query by committee, and density sampling, we can intelligently select instances for labeling, improving the performance of models on imbalanced datasets.