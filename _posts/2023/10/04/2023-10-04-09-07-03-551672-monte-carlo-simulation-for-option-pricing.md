---
layout: post
title: "[python] Monte Carlo simulation for option pricing"
description: " "
date: 2023-10-04
tags: [python]
comments: true
share: true
---

In the field of finance, option pricing is an important concept that involves calculating the value of a financial derivative, known as an option. One popular method to price options is through Monte Carlo simulations. In this article, we will explore how to use Monte Carlo simulation in Python to price options.

## Table of Contents

- [Background](#background)
- [Monte Carlo Simulation](#monte-carlo-simulation)
- [Python Implementation](#python-implementation)
- [Conclusion](#conclusion)

## Background

Options are financial contracts between two parties that give the buyer the right, but not the obligation, to buy or sell an asset at a predetermined price (known as the strike price) within a specific time period. The price of an option depends on various factors such as the underlying asset's price, volatility, interest rates, and time to expiration.

One approach to price options is the Monte Carlo simulation method, which involves randomly generating possible future prices of the underlying asset and calculating the payoff of the option for each scenario. By simulating a large number of such scenarios, we can estimate the expected value of the option.

## Monte Carlo Simulation

In Monte Carlo simulation, we simulate the movement of the underlying asset by assuming it follows a stochastic process, such as geometric Brownian motion. This process takes into account the underlying asset's current price, its volatility, and the time to expiration.

To simulate the future prices of the asset, we generate random numbers from a known distribution, such as a normal distribution, and use them to calculate the future asset prices. We repeat this simulation process many times to obtain a range of possible future prices.

For each simulated scenario, we calculate the payoff of the option based on its specific payoff formula. Finally, we take the average of all the payoffs to estimate the option's expected value.

## Python Implementation

Let's implement a simple Monte Carlo simulation for pricing a European call option. A European call option gives the buyer the right to buy the underlying asset at the strike price at expiration.

```python
import numpy as np

def monte_carlo_option_pricing(S, K, r, sigma, T, simulations):
    dt = T / 365
    S_t = S * np.exp((r - (sigma**2 / 2)) * dt +
                     sigma * np.sqrt(dt) * np.random.normal(0, 1, simulations))

    payoffs = np.maximum(S_t - K, 0)
    option_price = np.mean(payoffs) * np.exp(-r * T)

    return option_price

# Example usage
option_price = monte_carlo_option_pricing(S=100, K=110, r=0.05, sigma=0.2, T=30, simulations=100000)
print(f"Option price: {option_price}")
```

In this implementation, `S` represents the current price of the underlying asset, `K` is the strike price, `r` is the risk-free interest rate, `sigma` is the asset's volatility, `T` is the time to expiration in days, and `simulations` is the number of simulation iterations to perform.

We calculate the future prices of the asset `S_t` using the geometric Brownian motion equation and generate random numbers using `np.random.normal(0, 1, simulations)`. The payoffs are calculated as the maximum of zero and the difference between the asset price and the strike price. Finally, we estimate the option price by taking the average of the payoffs and discounting it to the present value using `np.exp(-r * T)`.

## Conclusion

Monte Carlo simulation is a powerful technique for pricing options, as it allows us to capture the uncertainty in the underlying asset's price movements. By randomly generating future scenarios and calculating the option payoffs, we can estimate the expected value of the option.

Python provides various libraries, such as NumPy, for implementing Monte Carlo simulations, making it accessible and efficient for option pricing. With this article as a starting point, you can further explore and customize Monte Carlo simulations for different types of options and financial models.