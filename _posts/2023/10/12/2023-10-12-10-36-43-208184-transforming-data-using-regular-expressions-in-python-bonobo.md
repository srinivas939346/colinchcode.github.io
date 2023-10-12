---
layout: post
title: "[python] Transforming data using regular expressions in Python Bonobo"
description: " "
date: 2023-10-12
tags: [python]
comments: true
share: true
---

Regular expressions are a powerful tool for pattern-matching and transforming data. In Python, one popular library for working with regular expressions is `re`. In this blog post, we will explore how to use regular expressions to transform data in the Python Bonobo framework.

## Table of Contents
- [Introduction to Python Bonobo](#introduction-to-python-bonobo)
- [Using regular expressions in Python Bonobo](#using-regular-expressions-in-python-bonobo)
- [Example: Transforming data with regular expressions](#example-transforming-data-with-regular-expressions)
- [Conclusion](#conclusion)

## Introduction to Python Bonobo

Python Bonobo is an easy-to-use and powerful ETL (Extract, Transform, Load) framework for Python. It allows you to build data pipelines by defining iterators that process data in a structured and scalable way. Bonobo supports various data sources and transformations to handle different data formats and scenarios.

## Using regular expressions in Python Bonobo

To use regular expressions in Python Bonobo, we need to import the `re` module. This module provides functions for matching and manipulating strings using regular expressions.

```python
import re
```

With the `re` module imported, we can use regular expressions within our Python Bonobo pipeline to transform data.

## Example: Transforming data with regular expressions

Let's consider a scenario where we have a CSV file containing customer data, and we want to transform the phone numbers in a standardized format using regular expressions.

Here's a sample data from the CSV file:

```
Customer Name,Phone Number
John Doe,(123) 456-7890
Jane Smith,987-654-3210
```

To transform the phone numbers into a standardized format, we can use regular expressions to remove any non-digit characters and format them like `###-###-####`. 

Here's an example Python Bonobo pipeline that performs this transformation:

```python
import bonobo

def transform_phone_numbers(row):
    phone_number = row['Phone Number']
    # Remove non-digit characters using regular expressions
    formatted_phone_number = re.sub(r'\D', '', phone_number)
    # Insert dashes at appropriate positions
    formatted_phone_number = re.sub(r'(\d{3})(\d{3})(\d{4})', r'\1-\2-\3', formatted_phone_number)
    row['Phone Number'] = formatted_phone_number
    yield row

def main():
    with bonobo.parse.CSV('customer_data.csv') as csv_file:
        # Skip the header row
        for row in csv_file[1:]:
            transformed_row = transform_phone_numbers(row)
            yield transformed_row

if __name__ == '__main__':
    bonobo.run(main)
```

In this example, the `transform_phone_numbers` function takes a row from the CSV file and performs the phone number transformation. The Bonobo pipeline reads the CSV file, skips the header row, and applies the `transform_phone_numbers` function to each subsequent row. The transformed rows are then yielded as output.

## Conclusion

Regular expressions are a powerful tool for transforming data in Python Bonobo. By using regular expressions, you can easily manipulate and extract relevant information from your data. In this blog post, we explored how to use regular expressions to transform data in Python Bonobo and provided a practical example.