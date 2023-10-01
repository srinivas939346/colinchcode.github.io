---
layout: post
title: "[python] Continuous integration and testing in Python"
description: " "
date: 2023-10-02
tags: [python]
comments: true
share: true
---

In software development, it's crucial to ensure that your code works as expected and doesn't introduce any regressions. This is where continuous integration and testing come into play. Continuous integration (CI) is the practice of frequently integrating code changes into a shared repository, and testing is the process of running automated tests to validate the code. In this blog post, we'll explore how to implement CI and testing in Python projects.

## Table of Contents
1. [What is Continuous Integration?](#what-is-continuous-integration)
2. [Why is Testing Important?](#why-is-testing-important)
3. [Setting Up Continuous Integration with GitHub Actions](#setting-up-continuous-integration-with-github-actions)
4. [Writing Automated Tests in Python](#writing-automated-tests-in-python)
5. [Running Tests Locally](#running-tests-locally)
6. [Conclusion](#conclusion)

## What is Continuous Integration? ##

Continuous Integration is a software development practice that involves merging code changes from multiple developers into a shared repository frequently. The primary goal is to catch integration issues early and ensure that there are no conflicts between different code branches. CI also helps in detecting issues related to build and dependencies early in the development cycle.

## Why is Testing Important? ##

Testing is an essential part of the software development process. It helps validate that the code behaves as expected, prevents regressions, and ensures that new features or bug fixes don't introduce unintended side effects. Automated testing in CI pipelines provides confidence in the code quality and reduces the risk of shipping broken or unstable software.

## Setting Up Continuous Integration with GitHub Actions ##

GitHub Actions is a powerful tool for automating CI/CD workflows. It allows you to create custom workflows using YAML to build, test, and deploy your software. Let's set up a basic CI workflow for a Python project:

```yaml
name: Continuous Integration

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: 3.9

    - name: Install dependencies
      run: pip install -r requirements.txt

    - name: Run tests
      run: python -m unittest discover -s tests

    - name: Report coverage
      run: |
        pip install coverage
        coverage run -m unittest discover -s tests
        coverage report
```

This workflow triggers on every push to the `main` branch, sets up Python, installs project dependencies, and runs the tests. Additionally, it reports the test coverage using the `coverage` package.

## Writing Automated Tests in Python ##

Python provides a rich set of testing frameworks such as `unittest`, `pytest`, and `nose`. Let's consider the `unittest` framework for writing our tests. It allows us to define test cases and run them as a suite.

```python
import unittest

class CalculatorTest(unittest.TestCase):
    def test_addition(self):
        self.assertEqual(2 + 2, 4)
    
    def test_subtraction(self):
        self.assertEqual(5 - 3, 2)

if __name__ == '__main__':
    unittest.main()
```

In the above example, we define a test case `CalculatorTest` and write two test methods `test_addition` and `test_subtraction`. We assert that certain expressions evaluate to the expected result using the `assertEqual` method. Running this file will execute the tests.

## Running Tests Locally ##

Running tests locally before pushing changes is a good practice to catch issues early. You can use the following command to run your tests:

```
python -m unittest discover -s tests
```

By running this command in the project's root directory, the test runner will discover and run all the tests in the `tests` directory.

## Conclusion ##

Continuous integration and testing are vital components of the software development process. They help in ensuring code quality, catching integration issues, and reducing the risk of shipping unstable software. By setting up CI workflows and writing automated tests in Python, you can streamline your development process and deliver reliable software.