---
layout: post
title: "[python] Extracting data from APIs with Python Bonobo"
description: " "
date: 2023-10-12
tags: [python]
comments: true
share: true
---

In today's world, where data is the key to unlocking valuable insights and making informed decisions, accessing data through APIs has become an integral part of many projects. Python, with its rich ecosystem of libraries, offers various tools to interact with APIs and extract the desired data. One such powerful library is **Bonobo**.

Bonobo is a lightweight Python ETL (Extract, Transform, Load) framework that simplifies the process of extracting data from different sources, transforming and manipulating it, and loading it into various destinations. In this blog post, we will explore how to use Bonobo to extract data from APIs.

## Installing Bonobo

Before we dive into using Bonobo, we need to install it. You can install Bonobo using pip by running the following command:

```python
pip install bonobo
```

## Creating an API Source

To extract data from an API, we need to define a source that retrieves the data from the API endpoints. Bonobo provides a `bonobo.Request` helper class to make API requests easily. Below is an example code snippet that demonstrates how to create an API source using Bonobo:

```python
import bonobo
import requests

def api_source():
    url = "https://api.example.com/data"
    response = requests.get(url)
    yield response.json()

graph = bonobo.Graph(api_source)
```

In this example, we define a function `api_source` that makes an HTTP GET request to the API's endpoint. We use the `requests` library to perform the request and `response.json()` to extract the data from the response in JSON format. The `yield` keyword is used to emit the extracted data as a generator.

## Transforming and Loading the Data

Once we have extracted the data from the API, we can use Bonobo's transform and load operations to modify and store the data as needed. These operations can include filtering, mapping, aggregating, joining, and more.

Here's an example code snippet that demonstrates a simple transformation and loading operation using Bonobo:

```python
import bonobo

def transform_and_load(data):
    # Data transformation logic
    transformed_data = [item["name"].upper() for item in data]

    # Load the transformed data to a destination
    with open("output.txt", "w") as file:
        for item in transformed_data:
            file.write(item + "\n")

graph = bonobo.Graph(api_source, transform_and_load)
```

In this example, we define a function `transform_and_load` that accepts the data extracted from the API source. We then transform the data by converting the "name" field of each item to uppercase. Finally, we load the transformed data by writing it to a text file named `output.txt`.

## Running the Bonobo Graph

To execute the Bonobo graph and start the extraction, transformation, and loading process, we need to run the graph using the `bonobo.run` function. Here's an example code snippet:

```python
if __name__ == "__main__":
    bonobo.run(graph)
```

By running the graph, Bonobo executes the defined steps sequentially, starting from the API source, performing any transformations, and finally loading the data to the destination.

## Conclusion

Bonobo provides a convenient and elegant way to extract data from APIs using Python. With its simple and intuitive interface, it saves developers time and effort in handling the complexities of data extraction and manipulation. By leveraging Bonobo's features, you can unleash the power of APIs and utilize their data to drive meaningful insights and create impactful applications.