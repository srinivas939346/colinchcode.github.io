---
layout: post
title: "[python] Fibonacci retracement strategy"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

## Introduction

In the world of technical analysis, the Fibonacci retracement strategy is a popular tool used by traders to determine potential levels of support and resistance in financial markets. The strategy is based on the Fibonacci sequence, a series of numbers in which each number is the sum of the two preceding numbers.

## Understanding Fibonacci Retracement

The Fibonacci retracement levels are horizontal lines that indicate areas of possible price reversal during a trending market. These levels are drawn based on key Fibonacci ratios, namely 23.6%, 38.2%, 50%, 61.8%, and 78.6%.

To apply the Fibonacci retracement strategy, you need to identify a recent trend in a financial instrument's price movement. Once the trend is established, you draw the Fibonacci retracement levels by connecting the high and low points of the trend.

## Usage of Fibonacci Retracement Levels

### 1. Support and Resistance Levels

The main objective of the Fibonacci retracement strategy is to determine potential support and resistance levels. Traders use these levels to identify entry and exit points for their trades. The 38.2% and 61.8% levels are typically considered significant resistance and support levels, respectively.

### 2. Price Corrections

Fibonacci retracement levels are often used to identify potential price correction levels during a trend. Traders look for price retracements that test these levels before the trend continues. The 50% level is considered an important level where price may reverse or resume its trend.

### 3. Trend Reversals

In some cases, Fibonacci retracement levels can help identify potential trend reversals. When prices break above or below the 78.6% level, it may be an indication that the current trend is weakening or reversing.

## Implementing Fibonacci Retracement in Python

To calculate Fibonacci retracement levels, we can write a simple Python function that takes the high and low values of a trend as inputs and returns the retracement levels. Here's an example:

```python
def fibonacci_retracement(high, low):
    fib_levels = [0, 23.6, 38.2, 50, 61.8, 78.6, 100]

    retracement_levels = []
    for level in fib_levels:
        retracement = low + (level/100) * (high - low)
        retracement_levels.append(retracement)

    return retracement_levels

# Example usage
high_point = 100
low_point = 80
retracement_levels = fibonacci_retracement(high_point, low_point)
print(retracement_levels)
```

This function calculates the Fibonacci retracement levels based on the high and low points of a trend. The `fib_levels` list contains the Fibonacci ratios in percentage form. The function then iterates through the list, calculates the retracement level using the formula, and appends it to the `retracement_levels` list. Finally, it returns the list of retracement levels.

## Conclusion

The Fibonacci retracement strategy is a useful tool in technical analysis for identifying potential support and resistance levels, price corrections, and trend reversals. By applying this strategy, traders can make more informed decisions when entering or exiting trades. Implementing the Fibonacci retracement strategy in Python allows for automation and flexibility in analyzing financial markets.