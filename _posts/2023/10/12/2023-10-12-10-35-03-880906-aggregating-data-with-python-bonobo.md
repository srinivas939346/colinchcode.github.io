---
layout: post
title: "[python] Aggregating data with Python Bonobo"
description: " "
date: 2023-10-12
tags: [python]
comments: true
share: true
---

In data processing pipelines, it is often necessary to aggregate data based on certain criteria. Python Bonobo, a lightweight ETL (Extract, Transform, Load) framework, provides an easy way to handle data aggregation tasks.

In this tutorial, we will explore how to use Python Bonobo to aggregate data. We will start by installing and setting up Bonobo, then we will build a simple aggregation pipeline using a sample dataset.

## Prerequisites

Before getting started, make sure you have the following prerequisites installed on your system:

- Python 3.x
- pip (python package installer)

You can install Bonobo using pip by running the following command:

```
pip install bonobo
```

## Setting up the pipeline

First, let's import the necessary modules in our Python script:

```python
import bonobo
```

Next, we need to define the transformation step that will perform the data aggregation. The transformation step will receive a stream of records and output aggregated data based on a specified key. Here is an example of a simple aggregation transformation step:

```python
def aggregate_by_key(row):
    # Extract the key from the row
    key = row['key']

    # Initialize an empty dictionary to store the aggregated data
    aggregated_data = {}

    # Check if the key already exists in the aggregated data dictionary
    if key in aggregated_data:
        # If it exists, increment the count
        aggregated_data[key]['count'] += 1
    else:
        # If it doesn't exist, initialize the count to 1
        aggregated_data[key] = {'count': 1}

    return aggregated_data
```

In our example, we assume that each row in the input stream has a 'key' field. We aggregate the data by counting the occurrences of each unique key and store the result in a dictionary.

Now, let's define the pipeline that will process the data. The pipeline consists of one source that generates the input data, one transformation step that performs the aggregation, and one sink that consumes the aggregated data. Here is an example of a simple pipeline:

```python
def generate_data():
    # This is a mock data generator function
    for i in range(10):
        yield {'key': i % 3}

def main():
    graph = bonobo.Graph(
        generate_data,
        aggregate_by_key,
        bonobo.PrettyPrinter(),
    )

    bonobo.run(graph)

if __name__ == '__main__':
    main()
```

In our example, the `generate_data` function generates a stream of dictionaries, where each dictionary contains a 'key' field. The `aggregate_by_key` function performs the aggregation based on the 'key' field. The `bonobo.PrettyPrinter()` sink function prints the aggregated data.

## Running the pipeline

Save the code to a file, for example `aggregation_pipeline.py`, and run the script using the command:

```
python aggregation_pipeline.py
```

You should see the aggregated data printed to the console.

## Conclusion

Python Bonobo provides a simple and efficient way to aggregate data in data processing pipelines. By defining the transformation step, you can easily perform various types of aggregations based on your specific requirements. You can explore more advanced features of Bonobo by referring to the official documentation.

Happy aggregating with Python Bonobo!