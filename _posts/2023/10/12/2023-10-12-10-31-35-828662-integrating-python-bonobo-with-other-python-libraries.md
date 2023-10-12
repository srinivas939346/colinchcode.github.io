---
layout: post
title: "[python] Integrating Python Bonobo with other Python libraries"
description: " "
date: 2023-10-12
tags: [python]
comments: true
share: true
---

Bonobo is a powerful Extract, Transform, Load (ETL) framework for Python that makes it easy to create data processing pipelines. By integrating Bonobo with other Python libraries, you can leverage their functionalities to enhance your data pipelines and make them more efficient.

In this blog post, we will explore how you can combine Bonobo with other popular Python libraries such as pandas, SQLAlchemy, and requests to perform sophisticated data operations within your pipelines.

## Table of Contents
1. [Introduction](#introduction)
2. [Integrating Bonobo with pandas](#integrating-bonobo-with-pandas)
3. [Integrating Bonobo with SQLAlchemy](#integrating-bonobo-with-sqlalchemy)
4. [Integrating Bonobo with requests](#integrating-bonobo-with-requests)
5. [Conclusion](#conclusion)

## Introduction<a name="introduction"></a>
Bonobo provides a flexible and intuitive way to create data pipelines by defining reusable functions as graph nodes and connecting them together. However, there are scenarios where you might need to leverage the features offered by other libraries to manipulate and process the data within your pipelines.

## Integrating Bonobo with pandas<a name="integrating-bonobo-with-pandas"></a>
[pandas](https://pandas.pydata.org/) is a powerful data manipulation library for Python. It provides high-performance data structures and data analysis tools. By integrating Bonobo with pandas, you can easily perform complex data transformations, filtering, and aggregation operations within your data pipelines.

To integrate Bonobo with pandas, you can define a Bonobo transform function that utilizes the pandas library to manipulate the data. Here's an example:

```python
import pandas as pd
import bonobo

def pandas_transform(row):
    # Convert the row to a pandas DataFrame
    df = pd.DataFrame([row])

    # Perform data manipulation operations using pandas
    df['new_column'] = df['existing_column'] * 2

    # Convert the updated DataFrame back to a dictionary
    updated_row = df.to_dict(orient='records')[0]
    return updated_row

def get_graph():
    graph = bonobo.Graph()

    graph.add_chain(
        bonobo.CsvReader('input.csv'),
        pandas_transform,
        bonobo.CsvWriter('output.csv')
    )

    return graph
```

Here, we define a `pandas_transform` function that takes a row as input, converts it to a pandas DataFrame, performs some data manipulation using pandas functions, and converts the updated DataFrame back to a dictionary. This function can then be used as a node in the Bonobo graph to perform pandas-based transformations on the data.

## Integrating Bonobo with SQLAlchemy<a name="integrating-bonobo-with-sqlalchemy"></a>
[SQLAlchemy](https://www.sqlalchemy.org/) is a popular SQL toolkit and Object-Relational Mapping (ORM) library for Python. It provides a set of high-level API for interacting with databases. By integrating Bonobo with SQLAlchemy, you can easily read data from databases, perform database operations, and write data back to the database within your Bonobo pipelines.

To integrate Bonobo with SQLAlchemy, you can define a Bonobo transform function that uses SQLAlchemy to interact with the database. Here's an example:

```python
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker
import bonobo

engine = create_engine('sqlite:///database.db')
Session = sessionmaker(bind=engine)

def sqlalchemy_transform(row):
    session = Session()

    # Perform database operations using SQLAlchemy
    # Example: session.query(Model).filter_by(key=value).update({column: new_value})

    session.commit()

    session.close()

def get_graph():
    graph = bonobo.Graph()

    graph.add_chain(
        bonobo.CsvReader('input.csv'),
        sqlalchemy_transform,
        bonobo.CsvWriter('output.csv')
    )

    return graph
```

Here, we define a `sqlalchemy_transform` function that creates a session using the SQLAlchemy sessionmaker and performs database operations using SQLAlchemy's ORM API. This function can then be used as a node in the Bonobo graph to interact with the database.

## Integrating Bonobo with requests<a name="integrating-bonobo-with-requests"></a>
[requests](https://docs.python-requests.org/en/latest/) is a popular library for making HTTP requests in Python. By integrating Bonobo with requests, you can perform HTTP requests within your Bonobo pipelines to retrieve data from APIs, web services, or other HTTP-based data sources.

To integrate Bonobo with requests, you can define a Bonobo transform function that uses requests to make HTTP requests and process the response. Here's an example:

```python
import requests
import bonobo

def requests_transform(row):
    url = row['api_url']
    response = requests.get(url)
    data = response.json()

    # Perform data processing using the response data

    return processed_data

def get_graph():
    graph = bonobo.Graph()

    graph.add_chain(
        bonobo.CsvReader('input.csv'),
        requests_transform,
        bonobo.CsvWriter('output.csv')
    )

    return graph
```

In this example, we define a `requests_transform` function that takes a row containing an API URL, makes an HTTP GET request using requests, and processes the response data. This function can then be used as a node in the Bonobo graph to make HTTP requests and process the data within your data pipeline.

## Conclusion<a name="conclusion"></a>
By integrating Bonobo with other Python libraries such as pandas, SQLAlchemy, and requests, you can leverage their functionalities to enhance your data processing pipelines. Whether you need to perform complex data transformations, interact with databases, or make HTTP requests, integrating Bonobo with these libraries allows you to achieve more efficient and powerful ETL operations.

Explore the documentation of Bonobo and the libraries you wish to integrate with for more detailed examples and advanced use cases. Happy ETL-ing!