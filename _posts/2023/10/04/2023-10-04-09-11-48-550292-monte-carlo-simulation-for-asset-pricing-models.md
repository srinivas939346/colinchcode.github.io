---
layout: post
title: "[python] Monte Carlo simulation for asset pricing models"
description: " "
date: 2023-10-04
tags: [python]
comments: true
share: true
---

Monte Carlo simulation is a powerful technique used in various fields, including finance, to model and analyze complex systems. In the context of asset pricing models, Monte Carlo simulation can be employed to forecast the future prices of financial assets and calculate their expected values.

In this blog post, we will explore how to use Monte Carlo simulation in Python to price financial assets based on classic asset pricing models such as Black-Scholes.

## Table of Contents
1. [Introduction to Monte Carlo Simulation](#introduction-to-monte-carlo-simulation)
2. [Asset Pricing Models](#asset-pricing-models)
3. [Implementing Monte Carlo Simulation](#implementing-monte-carlo-simulation)
4. [Conclusion](#conclusion)

## Introduction to Monte Carlo Simulation

Monte Carlo simulation is a computational technique that generates random samples within a given range to estimate the behavior of a system. In the context of financial asset pricing, Monte Carlo simulation involves generating multiple scenarios of future stock prices based on assumptions about volatility, risk-free rates, and other model parameters.

## Asset Pricing Models

One commonly used asset pricing model is the Black-Scholes model, which provides a mathematical framework for pricing options and calculating their expected values. The Black-Scholes model takes into account factors such as stock price, strike price, time to expiration, risk-free rate, and volatility.

Other asset pricing models include the Heston model, the Vasicek model, and the Cox-Ingersoll-Ross model. Each model has its own assumptions and equations to determine the price of financial assets.

## Implementing Monte Carlo Simulation

To demonstrate how to implement Monte Carlo simulation for asset pricing models, let's consider the Black-Scholes model. Here's a simple Python code snippet that uses Monte Carlo simulation to price a European call option:

```python
import numpy as np
from scipy.stats import norm

def black_scholes(S, K, r, sigma, T):
    """
    Calculate the price of a European call option using the Black-Scholes model.
    
    Parameters:
    S (float): current stock price
    K (float): strike price
    r (float): risk-free rate
    sigma (float): volatility
    T (float): time to expiration
    
    Returns:
    float: option price
    """
    # Generate random samples
    np.random.seed(42)
    z = np.random.standard_normal()
    
    # Calculate d1 and d2
    d1 = (np.log(S / K) + (r + 0.5 * sigma ** 2) * T) / (sigma * np.sqrt(T))
    d2 = d1 - sigma * np.sqrt(T)
    
    # Calculate option price
    call_price = S * norm.cdf(d1) - K * np.exp(-r * T) * norm.cdf(d2)
    
    return call_price

# Usage example
S = 100  # current stock price
K = 105  # strike price
r = 0.05  # risk-free rate
sigma = 0.2  # volatility
T = 1  # time to expiration

option_price = black_scholes(S, K, r, sigma, T)
print("Option price:", option_price)
```

In the above code, we use the `numpy` and `scipy` libraries to generate random samples and calculate the option price using the Black-Scholes formula. The `norm.cdf` function from `scipy.stats` is used to calculate the cumulative distribution function.

## Conclusion

Monte Carlo simulation is a valuable tool for pricing financial assets and estimating their expected values. By generating multiple scenarios and sampling from probability distributions, it provides a way to analyze the uncertainty and risk associated with asset prices. In this blog post, we explored how to implement Monte Carlo simulation in Python for asset pricing models. This is just a simple example, and there are many other ways to expand and improve upon this code.