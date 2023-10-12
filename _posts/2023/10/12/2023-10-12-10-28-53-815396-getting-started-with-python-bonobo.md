---
layout: post
title: "[python] Getting started with Python Bonobo"
description: " "
date: 2023-10-12
tags: [python]
comments: true
share: true
---

Python Bonobo is a lightweight and flexible Extract-Transform-Load (ETL) framework that allows you to easily process data in Python. Whether you need to extract data from various sources, transform it in any desired way, or load it into different systems, Bonobo provides a simple and intuitive way to achieve your ETL goals.

In this tutorial, we will walk you through the steps to get started with Python Bonobo and show you how to create a basic ETL pipeline.

## Table of Contents
1. [Installation](#installation)
2. [Creating an ETL Pipeline](#creating-an-etl-pipeline)
3. [Running the Pipeline](#running-the-pipeline)
4. [Conclusion](#conclusion)

## Installation

To install Bonobo, you can simply use `pip`:

```shell
pip install bonobo
```

## Creating an ETL Pipeline

First, let's import the necessary modules and define our pipeline. In this example, we will create a pipeline that extracts data from a CSV file, transforms it by adding a new calculated field, and then loads it into a SQLite database.

```python
import bonobo
import csv
import sqlite3

def extract():
    with open('data.csv') as file:
        reader = csv.reader(file)
        yield from reader

def transform(row):
    # Add a new field by performing some calculations
    row.append(int(row[1]) * 2)
    return row

def load(row):
    conn = sqlite3.connect('database.db')
    cursor = conn.cursor()
    cursor.execute("INSERT INTO my_table (col1, col2) VALUES (?, ?)", row)
    conn.commit()

graph = bonobo.Graph()
graph.add_chain(extract, transform, load)

if __name__ == "__main__":
    bonobo.run(graph)
```

In the code above, we define three functions: `extract`, `transform`, and `load`. The `extract` function reads data from a CSV file and yields each row. The `transform` function takes a row, performs some calculations, and returns the transformed row. The `load` function connects to a SQLite database and inserts the row into a table.

We then create a `bonobo.Graph` object and add our functions to create the ETL pipeline. Finally, we use `bonobo.run(graph)` to run the pipeline.

## Running the Pipeline

To run the pipeline, save the code in a file (e.g., `etl.py`) and execute it using the Python interpreter:

```shell
python etl.py
```

Make sure you have a `data.csv` file in the same directory with the data you want to process.

## Conclusion

Python Bonobo provides a simple and powerful way to create ETL pipelines in Python. In this tutorial, you learned how to install Bonobo and create a basic ETL pipeline. Now you can explore the various features and capabilities of Bonobo to tackle more complex ETL tasks. Happy coding!