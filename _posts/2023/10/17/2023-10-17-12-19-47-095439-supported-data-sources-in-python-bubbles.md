---
layout: post
title: "[python] Supported data sources in Python Bubbles."
description: " "
date: 2023-10-17
tags: [python]
comments: true
share: true
---

Python Bubbles is a powerful library that allows you to extract, manipulate, and analyze data in Python. It provides various options for retrieving data from different sources and supports a wide range of data formats. In this blog post, we will explore some of the supported data sources in Python Bubbles.

## Table of Contents
- [CSV Files](#csv-files)
- [Excel Files](#excel-files)
- [SQL Databases](#sql-databases)
- [APIs](#apis)

## CSV Files<a id="csv-files"></a>
CSV (Comma-Separated Values) files are a popular choice for storing tabular data. Python Bubbles provides convenient functions to read and write CSV files. You can easily open a CSV file, read its contents, perform operations on the data, and save the modified data back to a CSV file.

Here is an example of reading a CSV file using Python Bubbles:

```python
import bubbles as b

data = b.CSV("data.csv").read()
```

## Excel Files<a id="excel-files"></a>
Python Bubbles also supports reading and writing Excel files, which are commonly used for storing structured data. With Python Bubbles, you can extract data from specific sheets within an Excel file, manipulate the data, and save it back to the same or a different file.

Here is an example of reading an Excel file using Python Bubbles:

```python
import bubbles as b

data = b.Excel("data.xlsx").read(sheet="Sheet1")
```

## SQL Databases<a id="sql-databases"></a>
Python Bubbles integrates well with SQL databases, allowing you to connect to a database, execute queries, and retrieve data. Python Bubbles supports various SQL database engines such as SQLite, MySQL, PostgreSQL, and Oracle.

Here is an example of connecting to a SQLite database and executing a query using Python Bubbles:

```python
import bubbles as b

database = b.SQL("sqlite:///data.db")
query = "SELECT * FROM table_name"
data = database.execute(query)
```

## APIs<a id="apis"></a>
Python Bubbles provides a convenient way to retrieve data from APIs. You can make HTTP requests to APIs, parse the response, and extract the required data. Python Bubbles supports popular data formats such as JSON and XML, making it easy to work with API data.

Here is an example of retrieving data from a REST API using Python Bubbles:

```python
import bubbles as b

response = b.API("https://api.example.com/data").get()
data = response.json()
```

These are just a few examples of the supported data sources in Python Bubbles. The library offers many more options for working with data, including reading data from web pages, PDF files, and more. Python Bubbles makes it effortless to access and handle data in various formats, empowering you to perform in-depth analysis and uncover insights in your Python workflows.

## References
- [Python Bubbles Documentation](https://bubbles.readthedocs.io)
- [Python Bubbles GitHub Repository](https://github.com/python-bubbles/python-bubbles)