---
layout: post
title: "[python] Real-time data processing with Python Bonobo"
description: " "
date: 2023-10-12
tags: [python]
comments: true
share: true
---

In today's data-driven world, real-time data processing has become a necessity in various domains, such as financial analysis, IoT, and streaming applications. Python, being a versatile language, offers a range of libraries and frameworks to handle real-time data processing tasks efficiently. One such powerful library is **Bonobo**.

Bonobo is an open-source Python library designed for ETL (Extract, Transform, Load) operations. It provides a simple and intuitive way to process data in real-time, making it a popular choice among developers. In this blog post, we will explore how to use Bonobo for real-time data processing.

## Table of Contents

1. What is Bonobo?
2. Real-time Data Processing with Bonobo
3. Examples of Bonobo Pipelines
4. Conclusion

## 1. What is Bonobo?

**Bonobo** is a Python library that helps you build complex data pipeline workflows with ease. It enables you to define data processing tasks, such as data extraction, transformation, and loading, in a declarative way using Python generators.

With Bonobo, you can easily create a data flow that processes data in real-time, regardless of the input source (files, databases, APIs, etc.) or the output destination (databases, message queues, etc.). It allows you to focus on defining the data transformations rather than dealing with the implementation details.

## 2. Real-time Data Processing with Bonobo

To get started with Bonobo, you first need to install it using `pip`:

```
pip install bonobo
```

Once installed, you can import it in your Python script:

```python
import bonobo
```

Bonobo provides a set of decorators and functions that allow you to define your data processing pipeline. The pipeline is a sequence of transformation steps applied to the data in a specific order. These steps can be written as Python functions or classes.

Here is a simple example that illustrates how to use Bonobo to process data in real-time:

```python
import bonobo

def extract():
    yield 1
    yield 2
    yield 3

def transform(value):
    return value * 2

def load(value):
    print(value)

graph = bonobo.Graph(
    extract,
    transform,
    load,
)

if __name__ == '__main__':
    bonobo.run(graph)
```

In the above example, we define three functions: `extract()`, `transform()`, and `load()`. The `extract()` function yields some sample data, and the `transform()` function doubles each value. Finally, the `load()` function prints the transformed value.

We create a `bonobo.Graph` object that represents our pipeline by defining the order of steps in the processing chain. We then use `bonobo.run(graph)` to execute the pipeline.

When running the script, you will see the transformed values printed in the console:

```
2
4
6
```

Bonobo takes care of executing the steps in the correct order and passes the output of one step as the input to the next step, creating a seamless data processing flow.

## 3. Examples of Bonobo Pipelines

Bonobo provides a range of built-in transformations and tools to perform complex data processing tasks. Let's look at a couple of examples of how Bonobo can be used for real-time data processing.

### Example 1: Data Ingestion and Transformation

Suppose you want to ingest data from a CSV file, filter out certain rows based on specific conditions, transform the remaining data, and load it into a database. Here's an example of a Bonobo pipeline that accomplishes this task:

```python
import bonobo
import pandas as pd

def extract():
    df = pd.read_csv('data.csv')
    yield from df.iterrows()

def filter_and_transform(row):
    # Apply filtering logic
    if row['age'] >= 18:
        row['age'] -= 5
  
    # Apply transformation logic
    row['income'] = row['income'] * 2
    
    yield row

def load(row):
    # Save the transformed data to the database
    # ...

graph = bonobo.Graph(
    extract,
    filter_and_transform,
    load,
)

if __name__ == '__main__':
    bonobo.run(graph)
```

In this example, the `extract()` function reads the data from a CSV file using Pandas, and `yield from df.iterrows()` yields each row in the dataframe.

The `filter_and_transform()` function applies filtering and transformation logic to each row. The modified rows are then yielded for further processing.

Finally, the `load()` function takes the transformed rows and saves them to a database.

### Example 2: Real-time Twitter Stream Analysis

Bonobo also integrates well with streaming APIs, allowing you to perform real-time analysis on streams of data. Let's take an example of analyzing tweets in real-time using Bonobo and the Twitter API:

```python
import bonobo
import tweepy

def extract():
    # Authenticate with Twitter API
    auth = tweepy.OAuthHandler('consumer_key', 'consumer_secret')
    auth.set_access_token('access_token', 'access_token_secret')

    # Create a stream listener
    class TweetStreamListener(tweepy.StreamListener):
        def on_status(self, status):
            yield status.text

    listener = TweetStreamListener()
    stream = tweepy.Stream(auth=auth, listener=listener)

    # Start streaming tweets
    stream.filter(track=['python'])

def analyze_tweet(text):
    # Perform sentiment analysis or any other analysis
    # ...

def load(result):
    # Save analysis results to a database or file
    # ...

graph = bonobo.Graph(
    extract,
    analyze_tweet,
    load,
)

if __name__ == '__main__':
    bonobo.run(graph)
```

In this example, the `extract()` function authenticates with the Twitter API and sets up a stream listener. The `on_status()` method in the listener yields the text of each tweet received.

The `analyze_tweet()` function performs analysis on each tweet, such as sentiment analysis or any other required analysis.

Finally, the `load()` function saves the analysis results to a database or file.

## 4. Conclusion

Bonobo is a powerful Python library that simplifies the process of real-time data processing. Whether you are dealing with simple data transformations or complex streaming tasks, Bonobo provides an intuitive way to define and execute data processing pipelines.

In this blog post, we explored the basics of Bonobo and saw some practical examples of how it can be used for real-time data processing. Give Bonobo a try and unleash the full potential of your data processing tasks!