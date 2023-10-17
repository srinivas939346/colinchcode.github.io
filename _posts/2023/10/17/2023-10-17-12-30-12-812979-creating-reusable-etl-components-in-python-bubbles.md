---
layout: post
title: "[python] Creating reusable ETL components in Python Bubbles."
description: " "
date: 2023-10-17
tags: [python]
comments: true
share: true
---

ETL (Extract, Transform, Load) processes are an essential part of data engineering and data integration workflows. They help in extracting data from various sources, transforming it into a desired format, and loading it into a target database or system. In this blog post, we will explore how to build reusable ETL components using Python Bubbles.

## What is Python Bubbles?

Python Bubbles is a lightweight Python library that provides a simple and intuitive interface for building data pipelines. It allows you to define reusable components and connect them together to create ETL workflows. With Python Bubbles, you can easily separate the data extraction, transformation, and loading steps, making your code more modular and maintainable.

## Installing Python Bubbles

To get started with Python Bubbles, you need to install the library using pip:

```
pip install python-bubbles
```

## Building a Reusable ETL Component

Let's say we want to build a generic component for cleaning and transforming data. We can define a Python class that encapsulates this functionality. Here's an example:

```python
from bubbles.components import Component

class DataTransformer(Component):
    def __init__(self, transformation_func):
        super().__init__()
        self.transformation_func = transformation_func

    def run(self, data):
        transformed_data = self.transformation_func(data)
        self.emit(transformed_data)
```

In the above code, we define a `DataTransformer` class that extends the `Component` class provided by Python Bubbles. The `__init__` method initializes the class with a transformation function, which will be applied to the input data. The `run` method applies the transformation function to the input data and emits the transformed data using the `emit` method.

## Connecting Components to Build an ETL Workflow

Once we have defined our reusable component, we can connect multiple instances of it together to build a complete ETL workflow. Here's an example:

```python
from bubbles.workflow import Workflow

# Define the transformation functions
def remove_duplicates(data):
    # Remove duplicate records from the data
    return list(set(data))

def normalize_names(data):
    # Normalize names by converting them to lowercase
    return [name.lower() for name in data]

# Create instances of the DataTransformer component
remove_duplicates_component = DataTransformer(transformation_func=remove_duplicates)
normalize_names_component = DataTransformer(transformation_func=normalize_names)

# Create a workflow and connect the components
workflow = Workflow()
workflow.connect(remove_duplicates_component)
workflow.connect(normalize_names_component)

# Run the workflow
workflow.run(data=[1, 2, 3, 3, 4, 5, "John", "JANE", "john", "Jane"])
```

In the above code, we define two transformation functions: `remove_duplicates` and `normalize_names`. We then create instances of the `DataTransformer` component, passing the respective transformation functions. Finally, we create a workflow object, connect the components together, and run the workflow with some sample data.

## Conclusion

Python Bubbles provides a powerful yet simple way to build reusable ETL components and connect them together to create data pipelines. By separating the extraction, transformation, and loading steps, you can create more modular and maintainable code. Give Python Bubbles a try in your next data integration project, and experience the ease of building ETL workflows.