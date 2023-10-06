---
layout: post
title: "[python] Sequential A/B testing in Python"
description: " "
date: 2023-10-06
tags: [python]
comments: true
share: true
---

A/B testing is a widely used technique for comparing the effectiveness of two different versions of a webpage, ad, or other digital asset. However, traditional A/B testing methods can be inefficient and time-consuming, especially when the sample sizes are large.

One solution to this problem is sequential A/B testing, which allows for continual monitoring of the test results and early stopping if a significant difference is detected. In this blog post, we will explore how to implement sequential A/B testing in Python.

## Table of Contents
- [What is sequential A/B testing?](#what-is-sequential-ab-testing)
- [How does sequential A/B testing work?](#how-does-sequential-ab-testing-work)
- [Implementing sequential A/B testing in Python](#implementing-sequential-ab-testing-in-python)
- [Conclusion](#conclusion)

## What is sequential A/B testing?

Sequential A/B testing is an adaptive approach to A/B testing that allows for early stopping of the test if a significant difference between the two variants is detected. Rather than collecting a fixed sample size and then analyzing the results, sequential testing allows for continual monitoring of the data and making decisions based on interim results.

## How does sequential A/B testing work?

The basic idea behind sequential A/B testing is to define a stopping rule that determines when to stop the test and declare a winner. This stopping rule is typically based on a statistical test that checks if the difference between the two variants is statistically significant.

During the test, data is collected and the results are analyzed after each additional observation. If at any point the test statistic crosses a predetermined threshold, the test can be stopped early and a conclusion can be made.

## Implementing sequential A/B testing in Python

To implement sequential A/B testing in Python, we can use the `statsmodels.stats.proportion` module, which provides functions for conducting hypothesis tests and calculating confidence intervals for proportions.

First, we need to import the necessary modules:

```python
import numpy as np
from statsmodels.stats.proportion import proportions_ztest
```

Next, we define a function that performs the sequential A/B test:

```python
def sequential_ab_test(data_A, data_B, alpha=0.05):
    n_A = len(data_A)
    n_B = len(data_B)

    successes_A = np.cumsum(data_A)
    successes_B = np.cumsum(data_B)

    z_scores, p_values = proportions_ztest([successes_A, successes_B], [n_A, n_B])

    for i in range(len(p_values)):
        if p_values[i] <= alpha/(i+1):
            return i, p_values[i]

    return None, None
```

The `sequential_ab_test` function takes in two arrays `data_A` and `data_B` representing the success (1) or failure (0) of each observation in the A and B variants, respectively. The function calculates the cumulative number of successes for each variant and performs a sequential A/B test using the `proportions_ztest` function.

Finally, we can use the function to perform a sequential A/B test:

```python
data_A = [1, 0, 0, 1, 1, 0, 1, 0, 0, 0]
data_B = [0, 1, 0, 0, 1, 0, 1, 1, 0, 1]

winner, p_value = sequential_ab_test(data_A, data_B)

if winner is not None:
    print(f"Variant {winner+1} is the winner with p-value {p_value}")
else:
    print("No winner")
```

In this example, we have two variants (A and B) with 10 observations each. We pass the data arrays to the `sequential_ab_test` function, which returns the winning variant (if any) and the corresponding p-value.

## Conclusion

Sequential A/B testing is a powerful tool for efficiently comparing the performance of two variants in an A/B test. By continually monitoring the test results and making early stopping decisions, we can save time and resources. The implementation of sequential A/B testing in Python using `statsmodels` package provides a convenient way to analyze the results and obtain meaningful insights.