---
layout: post
title: "[python] Building a data warehouse with Python Bonobo"
description: " "
date: 2023-10-12
tags: [python]
comments: true
share: true
---

In today's data-driven world, data warehouses play a crucial role in storing, managing, and analyzing large volumes of structured and unstructured data. Python Bonobo is a powerful ETL (Extract, Transform, Load) framework that allows Python developers to build scalable and efficient data pipelines for data warehousing.

In this blog post, we will explore the basics of building a data warehouse using Python Bonobo. We will cover topics like data extraction, transformation, and loading into a data warehouse.

## Table of Contents
1. [What is Bonobo?](#what-is-bonobo)
2. [Data Extraction](#data-extraction)
3. [Data Transformation](#data-transformation)
4. [Data Loading](#data-loading)
5. [Conclusion](#conclusion)

## What is Bonobo?
Bonobo is an open-source, lightweight, and flexible ETL framework for Python. It provides a simple and intuitive API for building data pipelines, making it easier to extract data from various sources, transform it, and load it into a destination system like a data warehouse.

Bonobo follows the concept of treating data as a stream, where each transformation applied to the data is considered as a processing step in the pipeline. This stream-based approach allows for efficient processing of large datasets while keeping the memory consumption low.

## Data Extraction
The first step in building a data warehouse is extracting data from different sources. Bonobo provides a wide range of built-in extractors for reading data from various sources such as databases, files, or APIs.

Let's consider an example where we want to extract data from a MySQL database. You can use the `bonobo.mysql` module to configure the database connection and build an extraction pipeline. Here's an example code snippet:

```python
import bonobo
import bonobo.mysql

def extract_data():
    connection = bonobo.mysql.get_connection(
        host='localhost',
        user='username',
        password='password',
        database='my_database'
    )

    with connection.cursor() as cursor:
        cursor.execute('SELECT * FROM my_table')
        for row in cursor.fetchall():
            yield row

pipeline = bonobo.Pipeline(
    extract_data
)

if __name__ == '__main__':
    bonobo.run(pipeline)
```

In this example, we establish a connection to the MySQL database and execute a query to fetch data from a specific table. The `extract_data` function is a generator function that yields each row of data retrieved from the database. Finally, we create a Bonobo pipeline with the `extract_data` generator as the source.

## Data Transformation
Once the data is extracted, the next step involves transforming the data according to our requirements. Bonobo provides a variety of built-in transformations that can be applied to the data stream.

For example, let's say we want to clean and normalize the data before loading it into the data warehouse. We can use the `bonobo.Lambda` transformation to apply custom transformation functions to each data record. Here's an example:

```python
def clean_data(row):
    # Perform data cleaning and normalization
    cleaned_row = {
        'name': row['name'].strip(),
        'age': int(row['age']),
        'email': row['email'].lower(),
    }
    return cleaned_row

pipeline = bonobo.Pipeline(
    extract_data,
    bonobo.Lambda(clean_data),
    # Additional transformations...
)

if __name__ == '__main__':
    bonobo.run(pipeline)
```

In this example, the `clean_data` function takes a row of data and applies specific cleaning and normalization operations. The transformed data is then returned as a result. The `bonobo.Lambda` transformation allows us to apply this custom function to each data record in the pipeline.

## Data Loading
The final step in building a data warehouse is loading the transformed data into your chosen destination system. Bonobo provides various connectors for loading data into popular data warehouse platforms like PostgreSQL, MongoDB, Elasticsearch, etc.

Let's consider loading the transformed data into a PostgreSQL database. We can use the `bonobo.postgresql` module to configure the database connection and build a loading pipeline. Here's an example code snippet:

```python
import bonobo
import bonobo.postgresql

def load_data(row):
    connection = bonobo.postgresql.get_connection(
        host='localhost',
        port=5432,
        user='username',
        password='password',
        dbname='my_database'
    )

    with connection.cursor() as cursor:
        cursor.execute(
            'INSERT INTO my_table (name, age, email) VALUES (%s, %s, %s)',
            (row['name'], row['age'], row['email'])
        )
        connection.commit()

pipeline = bonobo.Pipeline(
    extract_data,
    bonobo.Lambda(clean_data),
    bonobo.Lambda(load_data),
)

if __name__ == '__main__':
    bonobo.run(pipeline)
```

In this example, we establish a connection to the PostgreSQL database and execute an `INSERT` query to load the transformed data into a specific table. The `load_data` function takes the transformed data as input and inserts it into the database using a cursor. Finally, we create the Bonobo pipeline with the `load_data` transformation added.

## Conclusion
Python Bonobo provides a highly flexible and scalable framework for building data warehouses. With its intuitive API and built-in transformations, it becomes effortless to extract, transform, and load data into your chosen destination system.

In this blog post, we covered the basics of building a data warehouse using Python Bonobo. We explored data extraction from MySQL, data transformation using custom functions, and data loading into PostgreSQL. With Bonobo, you have the power to create robust and efficient data pipelines for your data warehousing needs.