---
layout: post
title: "[python] Handling streaming data with Python Bonobo"
description: " "
date: 2023-10-12
tags: [python]
comments: true
share: true
---

With the increasing popularity of real-time data processing, it is essential to have tools and libraries that can handle streaming data efficiently. One such library in Python is Bonobo, a lightweight ETL (Extract, Transform, Load) framework that provides an easy and flexible way to process streaming data.

In this article, we will explore how to use Bonobo to handle streaming data in Python. We will cover its key features, show you how to set it up, and demonstrate some common use cases.

## Table of Contents
1. [What is Bonobo?](#what-is-bonobo)
2. [Installation](#installation)
3. [Creating a Simple Pipeline](#creating-a-simple-pipeline)
4. [Handling Streaming Data](#handling-streaming-data)
5. [Filtering and Transforming Data](#filtering-and-transforming-data)
6. [Conclusion](#conclusion)

## What is Bonobo?

Bonobo is a Python library that provides a simple and intuitive way to build data pipelines for processing streaming data. It is designed to be easy to use, yet powerful enough to handle complex data transformations.

Bonobo follows the concept of "transformation functions," where you define a series of transformations to apply to your data. It provides built-in functions for common tasks like reading from a file or database, performing data transformations, and writing to an output destination.

Bonobo also integrates seamlessly with other Python libraries and frameworks, making it a versatile tool for handling streaming data.

## Installation

To install Bonobo, you can use `pip` or your preferred package manager. Open your terminal or command prompt and use the following command:

```shell
pip install bonobo
```

Once Bonobo is installed, you're ready to start using it in your Python projects.

## Creating a Simple Pipeline

Let's start by creating a simple data pipeline using Bonobo. Open your Python environment or create a new Python file and import the necessary modules:

```python
import bonobo

def extract():
    yield 'Hello,'
    yield 'World!'
    
def transform(text):
    return text.upper()
    
def load(text):
    print(text)

def main():
    graph = bonobo.Graph(extract, transform, load)
    bonobo.run(graph)

if __name__ == "__main__":
    main()
```

In this example, we define three functions: `extract()`, `transform()`, and `load()`. The `extract()` function yields two strings, 'Hello,' and 'World!', which serves as our input data.

The `transform()` function converts the input text to uppercase using the `upper()` method. The transformed data is then passed to the `load()` function, which simply prints the data.

We create a `bonobo.Graph` object, passing our functions as arguments in the desired order. Finally, we call `bonobo.run(graph)` to start the data pipeline.

To execute the script, run the Python file, and you will see the transformed data printed to the console:

```shell
HELLO,
WORLD!
```

Congratulations! You have created and executed your first Bonobo data pipeline.

## Handling Streaming Data

Bonobo shines when it comes to handling streaming data. It provides several built-in components for reading from files, databases, and other input sources, making it easy to process data in real-time.

Here's an example of reading from a CSV file and printing the data:

```python
import bonobo

def extract():
    with open('data.csv', 'r') as file:
        for line in file:
            yield line.strip()

def load(line):
    print(line)

def main():
    graph = bonobo.Graph(extract, load)
    bonobo.run(graph)

if __name__ == "__main__":
    main()
```

In this example, we use the `open()` function to read from a CSV file called 'data.csv'. The `extract()` function iterates over each line in the file and yields the cleaned data.

The cleaned data is then passed to the `load()` function, which prints each line to the console.

## Filtering and Transforming Data

Bonobo provides a range of transformation functions that you can use to filter and transform your data. Let's see an example that demonstrates filtering and transforming data:

```python
import bonobo

def extract():
    yield 1
    yield 2
    yield 3
    yield 4
    yield 5

def is_even(x):
    return x % 2 == 0

def square(x):
    return x * x

def load(x):
    print(x)

def main():
    graph = bonobo.Graph(extract, is_even, square, load)
    bonobo.run(graph)

if __name__ == "__main__":
    main()
```

In this example, the `extract()` function yields a sequence of numbers from 1 to 5. The `is_even()` function filters out odd numbers by returning `True` only for even numbers.

The filtered data is passed to the `square()` function, which squares each number. Finally, the transformed data is printed using the `load()` function.

The output will be:

```shell
4
16
```

## Conclusion

In this article, we have explored the basics of handling streaming data with Python Bonobo. We have seen how to set up Bonobo, create a simple data pipeline, handle streaming data, and perform common data transformations.

Bonobo provides an elegant and powerful solution for processing streaming data in Python. Its simplicity and flexibility make it an excellent choice for a variety of real-time data processing tasks.

If you're looking to handle streaming data efficiently, give Bonobo a try and unlock its potential for your data processing needs.