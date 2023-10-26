---
layout: post
title: "[python] Handling cyclical features (e.g., time of day, day of the week)"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

When dealing with cyclical features, such as time of day or day of the week, it is important to properly account for the cyclic nature of the data. In this blog post, we will explore some common techniques used in Python to handle cyclical features.

## 1. Encoding Cyclical Features

One common approach to handle cyclical features is to encode them using trigonometric functions, such as sine and cosine. The idea behind this encoding is to represent a cyclical feature as a continuous variable that varies between -1 and 1 over one complete cycle.

For example, let's consider the time of day as a cyclical feature. We can represent it as two separate features: one encoded with sine function and the other with cosine function. This way, we can capture both the periodic nature and the phase of the feature.

```python
import numpy as np

def encode_cyclical_feature(value, period):
    sin_value = np.sin(2 * np.pi * value / period)
    cos_value = np.cos(2 * np.pi * value / period)
    return sin_value, cos_value

# Example usage
time_of_day = 14    # hour of the day (0-23)
sin_time, cos_time = encode_cyclical_feature(time_of_day, 24)
```

In the above code snippet, `time_of_day` is encoded as two separate variables: `sin_time` and `cos_time`. These variables capture the cyclic nature of the time of day feature.

## 2. Normalizing Cyclical Features

Another important step when dealing with cyclical features is to normalize them consistently across the entire dataset. Since cyclical features may have different ranges or periods, it is crucial to normalize them properly to ensure meaningful comparisons.

One common normalization technique is to rescale the encoded features to the range of 0 to 1. This can be done using min-max scaling:

```python
def normalize_cyclical_feature(value, period):
    min_value = 0
    max_value = period
    normalized_value = (value - min_value) / (max_value - min_value)
    return normalized_value

# Example usage
normalized_time = normalize_cyclical_feature(time_of_day, 24)
```

The `normalize_cyclical_feature` function takes the original cyclical feature value and its period as input. It then normalizes the value to the range of 0 to 1.

## Conclusion

Handling cyclical features in Python involves encoding them using trigonometric functions, such as sine and cosine, and normalizing them consistently across the dataset. These techniques help capture the cyclic nature of the features and ensure meaningful comparisons.

By properly handling cyclical features, you can improve the performance of machine learning models that rely on such features and gain better insights from your data.

**References:**

- [Encoding cyclical continuous features - 24-hour time data](https://datascience.stackexchange.com/questions/5990/encoding-cyclical-time-features-for-machine-learning-purposes)
- [Cyclic encoding and feature extraction](https://eigenfoo.xyz/cyclic-features/)