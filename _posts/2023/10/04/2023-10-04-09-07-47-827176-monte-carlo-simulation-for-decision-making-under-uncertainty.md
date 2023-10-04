---
layout: post
title: "[python] Monte Carlo simulation for decision-making under uncertainty"
description: " "
date: 2023-10-04
tags: [python]
comments: true
share: true
---

When making decisions in the real world, we often encounter situations where outcomes are uncertain. This uncertainty can arise due to various factors such as market fluctuations, employee performance, or natural disasters. To make informed decisions in the face of uncertainty, we can use Monte Carlo simulation.

Monte Carlo simulation is a computational technique that uses random sampling to estimate possible outcomes of a decision. It is particularly useful when dealing with complex systems that have a large number of variables and possible scenarios.

## How Monte Carlo Simulation Works

Monte Carlo simulation involves running multiple iterations of a model or algorithm using random input values. Each iteration represents a possible outcome of the decision being analyzed. By aggregating the results of all iterations, we can generate a probability distribution showing the likelihood of various outcomes.

Here is a simple example of Monte Carlo simulation in Python:

```python
import random

def simulate_sales(units_sold_mean, units_sold_stddev, unit_price_mean, unit_price_stddev, num_iterations):
    total_revenue = []
    
    for _ in range(num_iterations):
        units_sold = random.gauss(units_sold_mean, units_sold_stddev)
        unit_price = random.gauss(unit_price_mean, unit_price_stddev)
        revenue = units_sold * unit_price
        total_revenue.append(revenue)
    
    return total_revenue

# Example usage
units_sold_mean = 100
units_sold_stddev = 10
unit_price_mean = 20
unit_price_stddev = 2
num_iterations = 1000

revenues = simulate_sales(units_sold_mean, units_sold_stddev, unit_price_mean, unit_price_stddev, num_iterations)

# Analyze the results
average_revenue = sum(revenues) / num_iterations
max_revenue = max(revenues)
min_revenue = min(revenues)

print("Average revenue: $", average_revenue)
print("Max revenue: $", max_revenue)
print("Min revenue: $", min_revenue)
```

In this example, we simulate the sales of a product by generating random values for the number of units sold (`units_sold`) and the unit price (`unit_price`). We repeat this process for a given number of iterations and store the revenue generated in each iteration. Finally, we analyze the results by calculating the average, maximum, and minimum revenue.

## Benefits of Monte Carlo Simulation

Monte Carlo simulation offers several benefits in decision-making under uncertainty:

1. **Probabilistic analysis:** Monte Carlo simulation provides a probability distribution of outcomes, allowing decision-makers to assess the likelihood of different scenarios and make informed choices.

2. **Flexibility:** Monte Carlo simulations can be applied to a wide range of decision problems, from financial forecasting to project management.

3. **Complexity handling:** Monte Carlo simulation allows for the analysis of complex systems with multiple variables and interdependencies that cannot be easily modeled using traditional analytical methods.

4. **Sensitivity analysis:** By varying input values within predefined ranges, Monte Carlo simulation enables sensitivity analysis to identify key factors driving the outcomes.

Monte Carlo simulation is a powerful tool for decision-making under uncertainty. It helps decision-makers understand the range of possible outcomes and make better-informed choices. With the availability of computational resources and user-friendly libraries in programming languages like Python, implementing Monte Carlo simulations has become easier than ever.