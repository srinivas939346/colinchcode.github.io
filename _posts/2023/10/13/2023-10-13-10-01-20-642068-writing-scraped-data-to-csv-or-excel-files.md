---
layout: post
title: "[python] Writing scraped data to CSV or Excel files"
description: " "
date: 2023-10-13
tags: [python]
comments: true
share: true
---

Web scraping allows us to extract data from websites, but what can we do with that data? One common use case is to save the scraped data to a CSV (Comma Separated Values) or Excel file for further analysis or manipulation. In this tutorial, we will explore how to write scraped data to these file formats using Python.

## Table of Contents
- [Writing to CSV](#writing-to-csv)
  - [Using csv module](#using-csv-module)
  - [Using pandas library](#using-pandas-library)
- [Writing to Excel](#writing-to-excel)
  - [Using openpyxl library](#using-openpyxl-library)
  - [Using pandas library](#using-pandas-library-1)
- [Conclusion](#conclusion)
- [References](#references)

## Writing to CSV

### Using csv module

Python's `csv` module provides functionality for reading and writing CSV files. To write our scraped data to a CSV file, we can follow these steps:

1. Open the file in write mode and create a `csv.writer` object.
2. Write the header row (optional) using the `writerow()` method.
3. Write the data rows using the `writerows()` method.

Here's an example that demonstrates how to write scraped data to a CSV file using the `csv` module:

```python
import csv

# Scrape data and store it in a list of dictionaries
data = [{'name': 'John', 'age': 25}, {'name': 'Jane', 'age': 30}]

# Open the CSV file in write mode
with open('data.csv', 'w', newline='') as csvfile:
    # Create a csv.writer object
    writer = csv.writer(csvfile)

    # Write the header row
    writer.writerow(['Name', 'Age'])

    # Write the data rows
    writer.writerows([[record['name'], record['age']] for record in data])
```

The code above scrapes a list of dictionaries and writes the scraped data to a CSV file named `data.csv`.

### Using pandas library

The `pandas` library is a powerful tool for data manipulation and analysis in Python. It provides a DataFrame object that makes working with tabular data easy. To write scraped data to a CSV file using `pandas`, we can follow these steps:

1. Create a DataFrame from the scraped data.
2. Use the `to_csv()` method to save the DataFrame to a CSV file.

Here's an example that demonstrates how to write scraped data to a CSV file using the `pandas` library:

```python
import pandas as pd

# Scrape data and store it in a list of dictionaries
data = [{'name': 'John', 'age': 25}, {'name': 'Jane', 'age': 30}]

# Create a DataFrame from the data
df = pd.DataFrame(data)

# Save the DataFrame to a CSV file
df.to_csv('data.csv', index=False)
```

The code above scrapes data, creates a DataFrame from it, and saves the DataFrame to a CSV file named `data.csv`.

## Writing to Excel

### Using openpyxl library

The `openpyxl` library is a widely used Python library for manipulating Excel files. To write scraped data to an Excel file using `openpyxl`, we can follow these steps:

1. Create a Workbook object.
2. Create a Worksheet object.
3. Write the header row and data rows to the Worksheet object.
4. Save the Workbook to a file.

Here's an example that demonstrates how to write scraped data to an Excel file using the `openpyxl` library:

```python
from openpyxl import Workbook

# Scrape data and store it in a list of dictionaries
data = [{'name': 'John', 'age': 25}, {'name': 'Jane', 'age': 30}]

# Create a Workbook object
wb = Workbook()

# Create a Worksheet object
ws = wb.active

# Write the header row
ws.append(['Name', 'Age'])

# Write the data rows
for record in data:
    ws.append([record['name'], record['age']])

# Save the Workbook to a file
wb.save('data.xlsx')
```

The code above scrapes data, creates a Workbook object, writes the scraped data to a Worksheet object, and saves the Workbook to an Excel file named `data.xlsx`.

### Using pandas library

As mentioned before, `pandas` provides powerful tools for data manipulation. It also supports writing data to Excel files. To write scraped data to an Excel file using `pandas`, we can follow these steps:

1. Create a DataFrame from the scraped data.
2. Use the `to_excel()` method to save the DataFrame to an Excel file.

Here's an example that demonstrates how to write scraped data to an Excel file using the `pandas` library:

```python
import pandas as pd

# Scrape data and store it in a list of dictionaries
data = [{'name': 'John', 'age': 25}, {'name': 'Jane', 'age': 30}]

# Create a DataFrame from the data
df = pd.DataFrame(data)

# Save the DataFrame to an Excel file
df.to_excel('data.xlsx', index=False)
```

The code above scrapes data, creates a DataFrame from it, and saves the DataFrame to an Excel file named `data.xlsx`.

## Conclusion

In this tutorial, we have explored different methods for writing scraped data to CSV and Excel files using Python. Whether you choose to use the `csv` module or the `pandas` library, both options provide efficient ways to save your scraped data in easily readable formats. With this knowledge, you can now take your web scraping projects to the next level and unlock the power of data analysis and manipulation.

## References

- [Python csv module documentation](https://docs.python.org/3/library/csv.html)
- [pandas documentation](https://pandas.pydata.org/docs/)
- [openpyxl documentation](https://openpyxl.readthedocs.io/en/stable/)