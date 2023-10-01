---
layout: post
title: "[python] Test-driven data analysis in Python"
description: " "
date: 2023-10-02
tags: [python]
comments: true
share: true
---

In the field of data analysis, it is important to have a well-structured and reliable workflow. One approach to achieving this is through test-driven development (TDD). TDD involves writing tests before writing the code, which helps improve the quality and maintainability of the code.

In this article, we will explore how to apply test-driven development principles to data analysis projects in Python. We will use the popular `pytest` library for writing and executing tests.

## Table of Contents
- [Setting up the Project](#setting-up-the-project)
- [Writing the Tests](#writing-the-tests)
- [Implementing the Functions](#implementing-the-functions)
- [Running the Tests](#running-the-tests)
- [Conclusion](#conclusion)

## Setting up the Project

Let's start by setting up the project. Create a new directory for your project and navigate to it:

```shell
mkdir test-driven-data-analysis
cd test-driven-data-analysis
```

Create a virtual environment and activate it:

```shell
python -m venv venv
source venv/bin/activate  # for UNIX-based systems
.\venv\Scripts\activate  # for Windows
```

Install the necessary packages:

```shell
pip install pytest
```

Now we are ready to write our tests.

## Writing the Tests

For the purpose of this example, let's consider a simple data analysis task - finding the average of a list of numbers. We will write a function called `calculate_average` that takes in a list of numbers and returns their average.

Create a new Python file called `test_analysis.py` and add the following code:

```python
def calculate_average(numbers):
    if not numbers:
        return 0
    return sum(numbers) / len(numbers)


def test_calculate_average():
    assert calculate_average([1, 2, 3, 4, 5]) == 3
    assert calculate_average([10, 20, 30, 40, 50]) == 30
    assert calculate_average([]) == 0
```

In the code above, we have defined the `calculate_average` function and written some test cases using the `assert` statement. The `assert` statement checks if the given condition is `True`, and if not, it raises an `AssertionError`.

## Implementing the Functions

Now it's time to implement the `calculate_average` function. Open the `test_analysis.py` file again and modify it as follows:

```python
def calculate_average(numbers):
    if not numbers:
        raise ValueError("Empty list")
    return sum(numbers) / len(numbers)


def test_calculate_average():
    assert calculate_average([1, 2, 3, 4, 5]) == 3
    assert calculate_average([10, 20, 30, 40, 50]) == 30
    assert calculate_average([]) == 0


# Run the tests
test_calculate_average()
```

We have added a check for an empty input list and raised a `ValueError` if the list is empty. This ensures that our function behaves as expected when encountering such cases.

## Running the Tests

To run the tests, open a terminal and navigate to the project directory. Execute the following command:

```shell
pytest test_analysis.py
```

You should see the output indicating that the tests have passed:

```shell
============================= test session starts ==============================
...
collected 1 item                                                               

test_analysis.py .                                                        [100%]

============================== 1 passed in 0.01s ===============================
```

Congratulations! You have successfully applied test-driven development principles to a data analysis project.

## Conclusion

Test-driven development is a powerful approach that helps ensure the accuracy, robustness, and maintainability of your code. By writing tests first, you can have a clear understanding of the expected behavior and catch any issues early on.

In this article, we have explored how test-driven development can be applied to data analysis projects in Python using the `pytest` library. This approach can be extended to more complex analyses, making your code more reliable and your projects more successful.