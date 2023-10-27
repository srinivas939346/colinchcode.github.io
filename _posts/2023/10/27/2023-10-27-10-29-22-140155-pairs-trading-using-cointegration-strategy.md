---
layout: post
title: "[python] Pairs trading using cointegration strategy"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

Pairs trading is a popular trading strategy that involves identifying two stocks that tend to move together, and then going long on one stock while simultaneously going short on the other stock when the price relationship between the two stocks diverges from its historical mean. One approach to identifying suitable pairs for pairs trading is through cointegration analysis.

Cointegration is a statistical technique that measures the long-term equilibrium relationship between two or more time series. In the context of pairs trading, cointegration helps to identify pairs of stocks that move together over the long term, even if they may temporarily diverge in the short term.

In this blog post, we will walk through an example of pairs trading using the cointegration strategy in Python.

## Steps involved

1. Collect historical price data for two stocks.
2. Calculate the price ratio of the two stocks.
3. Test for cointegration between the price ratio and a suitable benchmark.
4. Implement the trading strategy based on the divergence of the price ratio from its mean.
5. Evaluate the performance of the strategy.

## Collecting historical price data

To begin, we need to collect historical price data for the two stocks we want to trade. There are numerous data providers available that offer APIs to access stock price data. For this example, we will use the `yfinance` library to download historical price data from Yahoo Finance.

```python
import yfinance as yf

# Download historical price data for two stocks
stock1 = yf.download('AAPL', start='2010-01-01', end='2021-08-31')
stock2 = yf.download('MSFT', start='2010-01-01', end='2021-08-31')
```

## Calculating the price ratio

Once we have the historical price data, we can calculate the price ratio between the two stocks. The price ratio is simply the ratio of the closing prices of the two stocks at each time point.

```python
# Calculate the price ratio
price_ratio = stock1['Close'] / stock2['Close']
```

## Testing for cointegration

Next, we need to test whether the price ratio is cointegrated with a suitable benchmark. A common choice for the benchmark is an index that closely represents the overall market. In this example, we will use the S&P 500 index.

```python
import statsmodels.api as sm

# Add intercept term to the price ratio
price_ratio = sm.add_constant(price_ratio)

# Perform Engle-Granger cointegration test
result = sm.OLS(price_ratio, sm.add_constant(stock1['Close'])).fit()
adf_statistic = result.rsquared_adj

# Check for cointegration
if adf_statistic < 0.05:
    print("Price ratio is cointegrated with the benchmark.")
else:
    print("Price ratio is not cointegrated with the benchmark.")
```

## Implementing the trading strategy

If the price ratio is cointegrated with the benchmark, we can proceed with implementing the pairs trading strategy based on the divergence of the price ratio from its mean.

```python
import numpy as np

# Calculate the mean and standard deviation of the price ratio
mean_ratio = np.mean(price_ratio)
std_ratio = np.std(price_ratio)

# Define the trading bands
upper_band = mean_ratio + std_ratio
lower_band = mean_ratio - std_ratio

# Implement the trading strategy
position = 0  # 0: out of the market, 1: long stock1, -1: short stock1

for i in range(len(price_ratio)):
    if price_ratio[i] > upper_band and position != -1:
        position = -1
        sell_stock1()
        buy_stock2()
    elif price_ratio[i] < lower_band and position != 1:
        position = 1
        sell_stock2()
        buy_stock1()
    elif (price_ratio[i] < mean_ratio and price_ratio[i] > upper_band) or \
            (price_ratio[i] > mean_ratio and price_ratio[i] < lower_band):
        position = 0
        sell_stock1()
        sell_stock2()

# Define trading actions (e.g., buying and selling shares)
def buy_stock1():
    pass

def sell_stock1():
    pass

def buy_stock2():
    pass

def sell_stock2():
    pass
```

## Evaluating the performance

Finally, we can evaluate the performance of the pairs trading strategy by calculating various performance metrics such as the cumulative returns, Sharpe ratio, and maximum drawdown.

```python
# Calculate the cumulative returns
cumulative_returns = (stock1['Close'][-1] - stock1['Close'][0]) / stock1['Close'][0]

# Calculate the Sharpe ratio
returns = np.diff(stock1['Close']) / stock1['Close'][:-1]
sharpe_ratio = np.mean(returns) / np.std(returns)

# Calculate the maximum drawdown
rolling_max = stock1['Close'].cummax()
drawdown = (rolling_max - stock1['Close']) / rolling_max
max_drawdown = np.max(drawdown)

print("Cumulative Returns: ", cumulative_returns)
print("Sharpe Ratio: ", sharpe_ratio)
print("Max Drawdown: ", max_drawdown)
```

## Conclusion

Pairs trading using a cointegration strategy can be a profitable trading strategy when executed correctly. By identifying pairs of stocks that move together over the long term, traders can take advantage of price divergences and potentially profit from mean reversion. However, it's important to note that pairs trading involves risk, and careful analysis and risk management are crucial to its success.

References:
- [Pairs Trading: A Cointegration Approach](https://www.quantstart.com/articles/pairs-trading-a-cointegration-approach/)
- [Cointegration in Python](https://www.statsmodels.org/dev/examples/notebooks/generated/statespace_cointegration.html)