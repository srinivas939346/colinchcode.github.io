---
layout: post
title: "[python] Extracting data with Python Bonobo"
description: " "
date: 2023-10-12
tags: [python]
comments: true
share: true
---

In this blog post, we will explore how to extract data using Python Bonobo, a lightweight ETL (Extract, Transform, Load) framework. Bonobo provides a simple and flexible way to extract data from various sources, such as files, databases, and APIs.

## Table of Contents
- [Introduction to Python Bonobo](#introduction-to-python-bonobo)
- [Installing Bonobo](#installing-bonobo)
- [Extracting Data from Files](#extracting-data-from-files)
- [Extracting Data from Databases](#extracting-data-from-databases)
- [Extracting Data from APIs](#extracting-data-from-apis)
- [Conclusion](#conclusion)

## Introduction to Python Bonobo

Bonobo is a Python library that allows you to create data pipelines for extracting, transforming, and loading data. It provides a simple API for defining pipelines using a functional programming style. Bonobo pipelines are composed of reusable functions, making it easy to build modular and scalable data extraction workflows.

## Installing Bonobo

To install Bonobo, you can use `pip`:

```python
pip install bonobo
```

Once installed, you can import Bonobo into your Python script:

```python
import bonobo
```

## Extracting Data from Files

Bonobo provides various connectors to extract data from different file formats such as CSV, JSON, and XML. Let's see an example of how to extract data from a CSV file:

```python
import bonobo

def extract_data():
    with open('data.csv') as file:
        for line in file:
            yield line.strip().split(',')
    
def main():
    graph = bonobo.Graph(
        bonobo.CsvReader('data.csv'),
        bonobo.PrettyPrinter()
    )
    bonobo.run(graph)

if __name__ == '__main__':
    main()
```

In this example, we define `extract_data()` as a generator function that reads lines from the CSV file and yields them one by one. We then create a Bonobo graph that consists of a `CsvReader` component, which reads the data from the file, and a `PrettyPrinter` component, which prints the extracted data. Finally, we run the graph using `bonobo.run()`.

## Extracting Data from Databases

Bonobo also provides connectors to extract data from databases such as MySQL, PostgreSQL, and SQLite. Here's an example of extracting data from a MySQL database:

```python
import bonobo
import pymysql.cursors

def extract_data():
    connection = pymysql.connect(
        host='localhost',
        user='root',
        password='password',
        database='mydatabase'
    )
    
    with connection.cursor() as cursor:
        cursor.execute('SELECT * FROM mytable')
        for row in cursor:
            yield row
    
    connection.close()

def main():
    graph = bonobo.Graph(
        extract_data,
        bonobo.PrettyPrinter()
    )
    bonobo.run(graph)

if __name__ == '__main__':
    main()
```

In this example, we define `extract_data()` as a generator function that connects to a MySQL database, executes a query, and yields the rows one by one. We then create a Bonobo graph that consists of the `extract_data` function and a `PrettyPrinter` component. Finally, we run the graph using `bonobo.run()`.

## Extracting Data from APIs

Bonobo also supports extracting data from APIs using the `Python requests` library. Here's an example of extracting data from a RESTful API:

```python
import bonobo
import requests

def extract_data():
    response = requests.get('https://api.example.com/data')
    if response.status_code == 200:
        data = response.json()
        for item in data:
            yield item
    
def main():
    graph = bonobo.Graph(
        extract_data,
        bonobo.PrettyPrinter()
    )
    bonobo.run(graph)

if __name__ == '__main__':
    main()
```

In this example, we define `extract_data()` as a generator function that sends a GET request to an API and yields the response data one by one. We then create a Bonobo graph that consists of the `extract_data` function and a `PrettyPrinter` component. Finally, we run the graph using `bonobo.run()`.

## Conclusion

Python Bonobo provides a powerful and flexible way to extract data from various sources. In this blog post, we explored how to extract data from files, databases, and APIs using Bonobo. With its simple and intuitive API, Bonobo makes it easy to build scalable and modular data extraction workflows. Give it a try in your next ETL project!