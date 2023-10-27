---
layout: post
title: "[python] Trend following strategy"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

Trend following is a popular investment strategy that follows the direction of a market trend. This strategy assumes that the current price trend will continue and seeks to capture profits by buying when the price is rising or selling short when the price is falling.

In this blog post, we will implement a simple trend following strategy using Python.

### Strategy Overview

The basic idea behind a trend following strategy is to identify when a market is in an uptrend or a downtrend. Once the trend is determined, we will take appropriate actions to capture profits.

### Technical Indicators

To determine the trend, we will use technical indicators such as moving averages. Moving averages smooth out the price data over a specified time period and help identify the overall direction of the market.

For our strategy, we will use two moving averages - a shorter-term moving average and a longer-term moving average. When the shorter-term moving average crosses above the longer-term moving average, it suggests an uptrend, and when it crosses below, it suggests a downtrend.

### Implementation

Let's implement the trend following strategy in Python:

```python
import pandas as pd

def trend_following_strategy(data, short_window=50, long_window=200):
    data['short_ma'] = data['close'].rolling(window=short_window).mean()
    data['long_ma'] = data['close'].rolling(window=long_window).mean()

    data['signal'] = 0
    data.loc[data['short_ma'] > data['long_ma'], 'signal'] = 1
    data.loc[data['short_ma'] < data['long_ma'], 'signal'] = -1

    return data

# Load historical price data
price_data = pd.read_csv('historical_data.csv')

# Apply trend following strategy
strategy_data = trend_following_strategy(price_data)

# Print the strategy data
print(strategy_data)
```

In this code snippet, we first import the necessary libraries and define the `trend_following_strategy` function. This function takes in the historical price data and calculates the shorter-term and longer-term moving averages.

We then initialize the 'signal' column with zeroes and update it based on the crossover of the moving averages. A value of 1 indicates an uptrend, -1 indicates a downtrend, and 0 indicates no clear trend.

Finally, we apply the strategy to the historical price data and print the resulting strategy data.

### Conclusion

Trend following strategies can be powerful tools for capturing profits in the financial markets. By identifying and following the trends, we can take advantage of market momentum and potentially achieve better investment returns.

While the strategy implemented in this blog post is a simple example, it can serve as a starting point for building more sophisticated trend following strategies. Remember to test and validate any trading strategy before applying it with real money.

References:
- [Investopedia - Trend Following Trading Strategy](https://www.investopedia.com/terms/t/trendfollowing.asp)
- [Pandas documentation](https://pandas.pydata.org/docs/)
- [Technical Analysis Library in Python (TA-Lib)](https://github.com/mrjbq7/ta-lib)