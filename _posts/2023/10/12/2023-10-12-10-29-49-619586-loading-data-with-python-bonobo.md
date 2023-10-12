---
layout: post
title: "[python] Loading data with Python Bonobo"
description: " "
date: 2023-10-12
tags: [python]
comments: true
share: true
---

Bonobo is a lightweight and flexible ETL (Extract, Transform, Load) framework for Python. With Bonobo, you can easily create data pipelines for loading, transforming, and processing data. In this blog post, we will focus on how to load data using Bonobo.

## Installation

To get started with Bonobo, you need to install it first. You can install Bonobo using pip by running the following command:

```
pip install bonobo
```

## Loading data from a file

Bonobo provides a variety of built-in file connectors to load data from various file formats such as CSV, Excel, JSON, etc. Let's see how to load data from a CSV file.

First, import the necessary modules:

```python
import bonobo
import csv
```

Next, define a function to load data from the CSV file:

```python
def load_data():
    with open('data.csv', 'r') as f:
        reader = csv.reader(f)
        for row in reader:
            yield row
```

Note that the `yield` statement is used to generate each row of data as a generator.

Finally, create a Bonobo graph that uses the `load_data` function as a source:

```python
def get_graph():
    graph = bonobo.Graph()
    graph.add_chain(load_data)
    return graph
```

You can now run the graph using the `bonobo.run()` function:

```python
if __name__ == '__main__':
    bonobo.run(get_graph())
```

This will load the data from the CSV file and process it further using the Bonobo graph.

## Conclusion

Loading data with Bonobo is easy and convenient. By using the built-in file connectors, you can easily load data from various file formats. Bonobo provides a powerful and flexible framework for building ETL pipelines in Python.