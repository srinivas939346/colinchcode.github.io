---
layout: post
title: "[python] Real-time data integration using Python Bonobo"
description: " "
date: 2023-10-12
tags: [python]
comments: true
share: true
---

In today's data-driven world, it's essential to have a robust and efficient way to integrate data from various sources in real-time. Python Bonobo is a lightweight yet powerful ETL (Extract, Transform, Load) framework that allows you to seamlessly integrate data from multiple sources.

In this blog post, we'll explore how to use Python Bonobo to build a real-time data integration pipeline.

## Table of Contents

1. Introduction
2. Setting up Bonobo
3. Extracting data from different sources
4. Transforming and enriching data
5. Loading data into a destination
6. Conclusion

## 1. Introduction

Python Bonobo provides a simple and intuitive way to build data processing pipelines. It's a minimalist framework that promotes a functional programming approach, allowing you to focus on the logic of your data integration rather than dealing with the complexities of the framework itself.

## 2. Setting up Bonobo

To get started with Bonobo, you'll need to install it using pip:

```
pip install bonobo
```

Once installed, you can create a new Python file and import the necessary modules:

```python
import bonobo
from bonobo.config import Configurable, ContextProcessor, Option
from bonobo.config import use_context
```

## 3. Extracting data from different sources

Bonobo provides various built-in components for extracting data from different sources, such as CSV files, databases, web APIs, and more. Let's take a look at an example of extracting data from a CSV file:

```python
@use_context
class CSVExtractor(Configurable):
    path = Option(str, required=True)

    @ContextProcessor
    def file(self, context):
        return open(self.path, 'r')

    def __call__(self, file):
        reader = csv.reader(file)
        for row in reader:
            yield {'data': row}

def extract_data():
    yield from CSVExtractor(path='data.csv')()
```

In this example, we define a custom extractor called `CSVExtractor` that accepts a file path as a parameter. We use the `ContextProcessor` decorator to open the file in the `file` context processor. The `__call__` method reads the CSV file row by row and yields each row as a dictionary.

## 4. Transforming and enriching data

Once we have extracted the data, we can perform various transformations and enrichments on it. Bonobo allows you to define transformation functions as separate Python functions or methods. Let's take a look at an example of transforming data:

```python

def transform_data(row):
    # Apply the transformation logic here
    transformed_row = {
        'data': row['data'].upper()
    }
    return transformed_row

def enrich_data(row):
    # Apply the enrichment logic here
    enriched_row = {
        'data': row['data'],
        'timestamp': datetime.datetime.now()
    }
    return enriched_row

def data_pipeline():
    yield from extract_data()
    yield from bonobo.Transform(transform_data)
    yield from bonobo.Transform(enrich_data)
```

In this example, we define two separate functions, `transform_data` and `enrich_data`, to perform the transformations and enrichments on the data. We then use the `bonobo.Transform` component to apply these functions in the data pipeline.

## 5. Loading data into a destination

Once the data is transformed and enriched, we can load it into a destination of our choice. Bonobo provides various built-in components for loading data into databases, files, or other external systems. Let's take a look at an example of loading data into a CSV file:

```python
@use_context
class CSVLoader(Configurable):
    path = Option(str, required=True)

    @ContextProcessor
    def file(self, context):
        return open(self.path, 'a')

    def __call__(self, file, *rows):
        writer = csv.writer(file)
        writer.writerows(rows)

def load_data():
    yield from data_pipeline()
    yield CSVLoader(path='output.csv')
```

In this example, we define a custom loader called `CSVLoader` that accepts a file path as a parameter. We use the `ContextProcessor` decorator to open the file in the `file` context processor. The `__call__` method takes the transformed and enriched rows as argument and writes them to the CSV file.

## 6. Conclusion

Python Bonobo is a powerful framework for building real-time data integration pipelines. In this blog post, we explored how to use Bonobo to extract data from different sources, transform and enrich the data, and load it into a destination. Bonobo's minimalist approach and intuitive API make it a great choice for data integration projects.

Next time you need to integrate real-time data, give Python Bonobo a try and see how it simplifies your ETL process.

Happy data integration!