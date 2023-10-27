---
layout: post
title: "[python] Relative strength index strategy"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

The Relative Strength Index (RSI) is a popular technical indicator used to identify overbought and oversold conditions in the market. Traders often incorporate RSI into their strategies to make buy or sell decisions.

In this article, we will discuss a simple RSI strategy using Python programming language. We will walk through the steps of implementing the strategy and provide example code to showcase its usage.

## What is the RSI?

The RSI is a momentum oscillator that measures the speed and change of price movements. It ranges from 0 to 100 and is typically displayed as a line graph on a chart. The RSI value above 70 indicates overbought conditions, while a value below 30 indicates oversold conditions.

## RSI Strategy

The RSI strategy involves buying or selling when the RSI crosses certain thresholds. Here's a simple RSI strategy:

1. Calculate the RSI using a specified period (typically 14 days).
2. Define the overbought and oversold thresholds (e.g., 70 and 30).
3. If the RSI crosses above the overbought threshold, sell or take a short position.
4. If the RSI crosses below the oversold threshold, buy or take a long position.
5. Monitor the RSI for further signals and repeat the process.

## Example Code

```python
import pandas as pd
import talib

# Get historical stock data
df = pd.read_csv('stock_data.csv')

# Calculate RSI
df['RSI'] = talib.RSI(df['Close'], timeperiod=14)

# Define overbought and oversold thresholds
overbought_threshold = 70
oversold_threshold = 30

# Buy or sell based on RSI thresholds
df['Signal'] = ''
df.loc[df['RSI'] > overbought_threshold, 'Signal'] = 'Sell'
df.loc[df['RSI'] < oversold_threshold, 'Signal'] = 'Buy'

# Print the signals
print(df[['Date', 'Close', 'RSI', 'Signal']])

```

In the above example code, we import the necessary libraries, read a CSV file containing historical stock data, calculate the RSI using the `talib` library, and define the overbought and oversold thresholds. We then assign a "Buy" or "Sell" signal based on the RSI values.

The final step is to print the signals, which show the date, closing price, RSI value, and the corresponding action (Buy or Sell).

## Conclusion

The RSI strategy is just one way to incorporate technical analysis into your trading decisions. By identifying overbought and oversold conditions, you can potentially improve the timing of your trades. However, it's important to note that no strategy guarantees profits and market conditions can change rapidly.

Please refer to the documentation of the tools and libraries used for a more detailed understanding of their functionalities.

**References:**
- [Relative Strength Index (RSI) - Investopedia](https://www.investopedia.com/terms/r/rsi.asp)
- [talib library - GitHub](https://github.com/mrjbq7/ta-lib)
- [Pandas library - Documentation](https://pandas.pydata.org/docs/)