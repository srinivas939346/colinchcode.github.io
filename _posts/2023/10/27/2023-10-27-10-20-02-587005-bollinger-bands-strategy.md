---
layout: post
title: "[python] Bollinger Bands strategy"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

In this article, we will explore the Bollinger Bands strategy, a popular technical analysis tool used by traders to identify potential buying and selling opportunities in financial markets. The Bollinger Bands strategy is based on the concept of volatility and uses two standard deviation lines along with a simple moving average to generate trading signals.

## What are Bollinger Bands?

Bollinger Bands are a technical analysis tool created by John Bollinger. They consist of three lines:

1. **Middle Band**: This is a simple moving average (SMA) usually set to a 20-period SMA.
2. **Upper Band**: This is the middle band plus two times the standard deviation of the price.
3. **Lower Band**: This is the middle band minus two times the standard deviation of the price.

The bands widen or narrow depending on market volatility. When the market is more volatile, the bands expand, and when it is less volatile, the bands contract.

## The Bollinger Bands Strategy

The Bollinger Bands strategy utilizes the upper and lower bands to identify potential entry and exit points in the market. 

The following are the key components of the strategy:

1. **Buy Signal**: A buy signal is generated when the price touches or crosses the lower band, indicating that the price may have reached a support level and a potential reversal or bounce upwards may occur.
2. **Sell Signal**: A sell signal is generated when the price touches or crosses the upper band, indicating that the price may have reached a resistance level and a potential reversal or decline may occur.
3. **Confirmation**: Traders often use additional indicators or confirmation signals to validate the Bollinger Bands signals before executing trades.

## Example Code

```python
import pandas as pd
from matplotlib import pyplot as plt

def bollinger_bands_strategy(df, window=20, std_multiplier=2):
    df['SMA'] = df['Close'].rolling(window=window).mean()
    df['Upper Band'] = df['SMA'] + std_multiplier * df['Close'].rolling(window=window).std()
    df['Lower Band'] = df['SMA'] - std_multiplier * df['Close'].rolling(window=window).std()

    # Generate signals
    df['Buy Signal'] = df['Close'] < df['Lower Band']
    df['Sell Signal'] = df['Close'] > df['Upper Band']

    # Plotting
    plt.figure(figsize=(12, 6))
    plt.plot(df['Close'], label='Close Price')
    plt.plot(df['SMA'], label='SMA')
    plt.plot(df['Upper Band'], label='Upper Band')
    plt.plot(df['Lower Band'], label='Lower Band')
    plt.scatter(df[df['Buy Signal']].index, df[df['Buy Signal']]['Close'], color='green', marker='^', label='Buy Signal')
    plt.scatter(df[df['Sell Signal']].index, df[df['Sell Signal']]['Close'], color='red', marker='v', label='Sell Signal')
    plt.title('Bollinger Bands Strategy')
    plt.xlabel('Date')
    plt.ylabel('Price')
    plt.legend()
    plt.show()

# Usage example
data = pd.read_csv('stock_data.csv')
bollinger_bands_strategy(data)
```

In this example, we define a function `bollinger_bands_strategy` that takes in a pandas DataFrame containing stock price data. It calculates the moving average, upper band, and lower band using the given window size and standard deviation multiplier. It then generates buy and sell signals based on the Bollinger Bands strategy. Finally, it plots the stock price along with the moving average and Bollinger Bands, highlighting the buy and sell signals.

## Conclusion

The Bollinger Bands strategy is a widely used tool for traders to identify potential buying and selling opportunities in financial markets. By understanding the concept of volatility and using the upper and lower bands as signals, traders can make more informed decisions. However, it is important to note that the Bollinger Bands strategy should not be used in isolation and should be combined with other indicators or confirmation signals for better accuracy.

If you want to learn more about Bollinger Bands, you can refer to the official documentation by [John Bollinger](https://www.bollingerbands.com/).

Remember to backtest and validate any trading strategy before deploying it in real market conditions.