---
layout: post
title: "[python] Transforming data with Python Bonobo"
description: " "
date: 2023-10-12
tags: [python]
comments: true
share: true
---

Python Bonobo is a lightweight and easy-to-use ETL (Extract, Transform, Load) framework that allows you to transform data in Python. In this blog post, we will explore how to use Bonobo to transform data efficiently.

## Table of Contents
1. [Introduction to Bonobo](#introduction-to-bonobo)
2. [Installation](#installation)
3. [Transforming Data](#transforming-data)
4. [Conclusion](#conclusion)

## Introduction to Bonobo

Bonobo is a Python framework that simplifies the ETL process by providing an intuitive and flexible API. It helps in handling large datasets and streamlining the data transformation process. Bonobo allows you to define a data pipeline using simple Python functions, which makes it easy to understand and maintain.

## Installation

To install Bonobo, you can use pip:

```shell
pip install bonobo
```

Once installed, you can import it into your Python script:

```python
import bonobo
```

## Transforming Data

Bonobo provides various transformation functions that you can use to process your data. Let's look at some common data transformations you can perform with Bonobo:

### Filter Data

Bonobo provides a `Filter` transformation that allows you to filter out specific data based on a condition. Here's an example:

```python
def filter_data(*args):
    for data in args:
        if data['age'] > 18:
            yield data

graph = bonobo.Graph(
    bonobo.CsvReader('input.csv'),
    filter_data,
    bonobo.JsonWriter('output.json')
)
```

This example filters out data for individuals who are above 18 years of age.

### Map Data

Bonobo provides a `Map` transformation that allows you to apply a function to each element of your data. Here's an example:

```python
def square_age(*args):
    for data in args:
        data['age'] = data['age'] ** 2
        yield data

graph = bonobo.Graph(
    bonobo.CsvReader('input.csv'),
    square_age,
    bonobo.JsonWriter('output.json')
)
```

This example squares the age of each individual in the input data.

### Aggregate Data

Bonobo provides an `Aggregate` transformation that allows you to aggregate data based on a specific criteria. Here's an example:

```python
def aggregate_data(*args):
    agg_data = {}
    for data in args:
        country = data['country']
        if country in agg_data:
            agg_data[country] += data['population']
        else:
            agg_data[country] = data['population']
    
    for country, population in agg_data.items():
        yield {'country': country, 'population': population}

graph = bonobo.Graph(
    bonobo.CsvReader('input.csv'),
    aggregate_data,
    bonobo.JsonWriter('output.json')
)
```

This example aggregates the population data based on the country in the input data.

## Conclusion

Python Bonobo is a powerful and versatile framework for transforming data. In this blog post, we explored some common data transformations you can perform with Bonobo. Remember to install Bonobo using pip before getting started.