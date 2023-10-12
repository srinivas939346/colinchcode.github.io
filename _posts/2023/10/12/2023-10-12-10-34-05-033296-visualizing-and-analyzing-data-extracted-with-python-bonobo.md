---
layout: post
title: "[python] Visualizing and analyzing data extracted with Python Bonobo"
description: " "
date: 2023-10-12
tags: [python]
comments: true
share: true
---

## Introduction

Python Bonobo is a powerful Python library that helps in creating data pipelines for data extraction, transformation, and loading tasks. It provides a simple and intuitive way to process data by using **pipelines**. In this blog post, we will explore how to extract data using Bonobo and then visualize and analyze it using popular Python libraries such as Pandas and Matplotlib.

## Table of Contents

- [What is Python Bonobo?](#what-is-python-bonobo)
- [Installing Bonobo](#installing-bonobo)
- [Data Extraction with Bonobo](#data-extraction-with-bonobo)
- [Data Visualization with Pandas](#data-visualization-with-pandas)
- [Data Analysis with Matplotlib](#data-analysis-with-matplotlib)
- [Conclusion](#conclusion)

## What is Python Bonobo?

**Python Bonobo** is a lightweight and easy-to-use library for building ETL (Extract, Transform, Load) pipelines in Python. It simplifies the process of data extraction and transformation by providing a declarative and functional approach. Bonobo pipelines can be used to handle various data sources, such as files, databases, REST APIs, and more.

## Installing Bonobo

To get started with Bonobo, you need to install it first. You can install Bonobo using pip, by running the following command in your terminal:

```shell
pip install bonobo
```

## Data Extraction with Bonobo

Bonobo provides an easy way to extract data from various sources. Let's say we want to extract data from a CSV file. Here's an example of how to do it using Bonobo:

```python
import bonobo

def extract():
    with open('data.csv', 'r') as file:
        for line in file:
            yield line.strip().split(',')

graph = bonobo.Graph(
    bonobo.CsvReader('data.csv'),
    bonobo.PrettyPrinter(),
)

if __name__ == '__main__':
    bonobo.run(graph)
```

In this example, we define an `extract()` function that reads the CSV file line by line and yields rows as lists. We then create a Bonobo graph by chaining the `bonobo.CsvReader` and `bonobo.PrettyPrinter` operators. The `bonobo.run()` function executes the graph and prints the extracted data.

## Data Visualization with Pandas

Once we have the data extracted, we can use the powerful **Pandas** library for data manipulation and analysis. Pandas provides a wide range of functions and methods to work with structured data. Here's an example of how to load the extracted data into a Pandas DataFrame and visualize it:

```python
import pandas as pd

# Load data into a Pandas DataFrame
data = pd.read_csv('data.csv')

# Visualize data using Pandas
data.plot(kind='bar', x='column1', y='column2')

# Show the plot
plt.show()
```

In this example, we use the `pd.read_csv()` function to load the extracted data into a Pandas DataFrame. We can then use various plotting functions provided by Pandas, such as `plot()`, to visualize the data. Finally, we call `plt.show()` to display the plot.

## Data Analysis with Matplotlib

Apart from visualization, we can also perform data analysis using **Matplotlib**. Matplotlib is a popular plotting library in Python that allows you to create a wide range of plots, such as line plots, scatter plots, histograms, etc. Here's an example of how to analyze the extracted data using Matplotlib:

```python
import matplotlib.pyplot as plt

# Load data into a Pandas DataFrame
data = pd.read_csv('data.csv')

# Perform data analysis using Matplotlib
plt.hist(data['column1'])
plt.xlabel('X-axis label')
plt.ylabel('Y-axis label')
plt.title('Data Histogram')

# Show the plot
plt.show()
```

In this example, we load the extracted data into a Pandas DataFrame and then use Matplotlib's `hist()` function to create a histogram of one of the columns. We can customize the plot by adding labels to the axes and a title. Finally, we call `plt.show()` to display the plot.

## Conclusion

In this blog post, we explored how to extract data using Python Bonobo and then visualize and analyze it using Pandas and Matplotlib. Python Bonobo provides a simple and intuitive way to create data pipelines, making it easier to handle data extraction and transformation tasks. By combining Bonobo with Pandas and Matplotlib, we can efficiently process and analyze data in Python.