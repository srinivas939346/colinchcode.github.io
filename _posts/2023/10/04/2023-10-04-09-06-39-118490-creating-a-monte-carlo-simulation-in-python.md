---
layout: post
title: "[python] Creating a Monte Carlo simulation in Python"
description: " "
date: 2023-10-04
tags: [python]
comments: true
share: true
---

Monte Carlo simulation is a powerful technique used for solving problems through statistical sampling. It is commonly used in fields such as finance, engineering, and physics to model and simulate complex systems.

In this tutorial, we will walk through the process of creating a Monte Carlo simulation in Python. We will use the example of estimating the value of pi using the Monte Carlo method.

## Table of Contents
1. [What is Monte Carlo Simulation?](#what-is-monte-carlo-simulation)
2. [Estimating Pi using Monte Carlo Method](#estimating-pi-using-monte-carlo-method)
3. [Implementation in Python](#implementation-in-python)
4. [Conclusion](#conclusion)

## What is Monte Carlo Simulation?
Monte Carlo simulation is a computational technique that uses random sampling to solve complex problems. It involves running multiple simulations using random inputs and observing the outcomes. By repeating this process numerous times, we can estimate the probability distributions and expected values of uncertain variables.

## Estimating Pi using Monte Carlo Method
One classic example of a Monte Carlo simulation is estimating the value of pi. The basic idea is as follows:

- Consider a square with side length 2 units, centered at the origin.
- Inscribe a circle within this square, touching the edges.
- Randomly generate points within the square and count the number of points that fall inside the circle.
- The ratio of the points inside the circle to the total number of points will approach π/4 as the number of samples increases.
- Finally, we can estimate the value of pi by multiplying the ratio by 4.

## Implementation in Python
Let's now implement the Monte Carlo simulation to estimate the value of pi in Python:

```python
import random

def estimate_pi(num_samples):
    points_inside_circle = 0
    points_inside_square = 0

    for _ in range(num_samples):
        x = random.uniform(-1, 1)
        y = random.uniform(-1, 1)

        distance = x**2 + y**2

        if distance <= 1:
            points_inside_circle += 1

        points_inside_square += 1

    ratio = points_inside_circle / points_inside_square
    pi_estimate = 4 * ratio

    return pi_estimate

# Running the simulation with 1 million samples
pi_estimate = estimate_pi(1000000)
print(f"Estimated value of pi: {pi_estimate}")
```

In the above code, we define a function called `estimate_pi` that takes the number of samples as input. We generate random x and y coordinates within the range [-1, 1] and calculate the distance from the origin. If the distance is less than or equal to 1, the point falls inside the circle. We keep track of the number of points inside the circle and the total number of points. Finally, we calculate the ratio and estimate the value of pi.

## Conclusion
Monte Carlo simulation is a versatile tool that allows us to solve a wide range of problems through random sampling. In this tutorial, we covered the basics of Monte Carlo simulation and how to implement it in Python to estimate the value of pi. Feel free to explore further and apply this technique to various other problem domains.