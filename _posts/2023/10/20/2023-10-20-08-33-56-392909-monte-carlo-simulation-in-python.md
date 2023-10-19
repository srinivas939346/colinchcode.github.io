---
layout: post
title: "[python] Monte Carlo simulation in Python"
description: " "
date: 2023-10-20
tags: [python]
comments: true
share: true
---

Monte Carlo simulation is a statistical method that allows you to model and analyze complex systems or problems using random sampling. It is widely used in various fields including finance, physics, and engineering.

In this blog post, we will walk you through the process of implementing a Monte Carlo simulation in Python. We will use a simple example of estimating the value of π (pi) using a circle and a square.

## Problem Description

The problem is to estimate the value of π by randomly generating points within a square and determining the proportion of points that fall within a quarter of a circle inscribed within the square.

![Monte Carlo Simulation](monte_carlo_simulation.png)

## Algorithm

Here is the algorithm we will follow for the Monte Carlo simulation:

1. Generate random (x, y) points within the square.
2. Compute the distance of each point from the origin (0, 0).
3. Check if the point lies within the quarter of a circle (using Pythagorean theorem).
4. Count the number of points that fall within the quarter of a circle.
5. Calculate the estimate of π using the formula: 4 * (number of points in quarter circle) / (total number of points).

## Python Implementation

Now, let's look at the Python code to implement the Monte Carlo simulation:

```python
import random

def estimate_pi(n):
    points_in_circle = 0
    total_points = 0

    for _ in range(n):
        x = random.uniform(-1, 1)
        y = random.uniform(-1, 1)
        distance = x**2 + y**2

        if distance <= 1:
            points_in_circle += 1

        total_points += 1

    pi = 4 * (points_in_circle / total_points)

    return pi

# Run the simulation with 1 million points
print("Estimated value of π:", estimate_pi(1000000))
```

## Explanation

In the code snippet above, we define a function called `estimate_pi` that takes an integer `n` as the number of points to generate for the simulation. We initialize two variables, `points_in_circle` and `total_points`, to keep track of the number of points that fall within the quarter of a circle and the total number of points generated, respectively.

We then loop `n` times and generate random `(x, y)` points within the square using the `random.uniform` function. We calculate the distance of each point from the origin using the Pythagorean theorem formula: `distance = x**2 + y**2`.

If the distance is less than or equal to 1 (i.e., the point falls within the quarter of a circle), we increment the `points_in_circle` counter. Regardless, we increment the `total_points` counter.

Finally, we calculate the estimate of π using the formula mentioned earlier and return the result.

## Conclusion

Monte Carlo simulation is a powerful technique to estimate unknown values or analyze complex systems using random sampling. In this blog post, we implemented a simple Monte Carlo simulation in Python to estimate the value of π. You can modify the code to experiment with different values of `n` for more accurate estimations.

References:
- [Monte Carlo method](https://en.wikipedia.org/wiki/Monte_Carlo_method)
- [Monte Carlo simulation](https://www.investopedia.com/terms/m/montecarlosimulation.asp)