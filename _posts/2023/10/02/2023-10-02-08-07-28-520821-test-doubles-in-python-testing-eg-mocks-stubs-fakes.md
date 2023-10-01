---
layout: post
title: "[python] Test doubles in Python testing (e.g., mocks, stubs, fakes)"
description: " "
date: 2023-10-02
tags: [python]
comments: true
share: true
---

In the world of software testing, it is common to face situations where we need to isolate the code under test from its dependencies or external systems. This is where test doubles come into play - they are objects that act as replacements for the real dependencies, allowing us to control their behavior during testing.

In this article, we will explore the various types of test doubles available in Python testing, including mocks, stubs, and fakes.

## Table of Contents
- [Mocks](#mocks)
- [Stubs](#stubs)
- [Fakes](#fakes)

## Mocks
Mocks are objects that simulate the behavior of real objects. They typically allow us to define expectations about method calls and return values, and can raise exceptions when specific conditions are met. In Python, there are several mocking frameworks available, such as `unittest.mock` (built-in since Python 3.3) and `pytest-mock` (a pytest plugin).

Here's an example of using `unittest.mock` to create a mock object:

```python
from unittest.mock import Mock

# Create a mock object
mock_obj = Mock()

# Define expectations
mock_obj.some_method.return_value = 42

# Interact with the mock object
result = mock_obj.some_method()
print(result)  # Output: 42

# Verify method calls
mock_obj.some_method.assert_called_once()
```

Mocks are useful when we want to verify that certain methods are called with specific parameters or to simulate different scenarios during testing.

## Stubs
Stubs are simpler versions of mocks that provide predetermined responses to method calls. They do not record method invocations or verify expectations. Stubs are often used to replace external dependencies or complex objects that are difficult to create in a test environment.

In Python, we can easily create stubs by defining functions or using the `unittest.mock` library:

```python
from unittest.mock import MagicMock

# Define a stub function
def stub_function():
    return 42

# Create a stub object using MagicMock
stub_obj = MagicMock(return_value=42)

# Interact with the stub object
result = stub_obj()
print(result)  # Output: 42
```

Stubs are useful when we don't care about the internal details of the dependency and just need it to return a specific value for testing purposes.

## Fakes
Fakes are test doubles that have a simplified implementation of the real dependencies. They are typically used when the real implementation is unavailable or too complex to use in a test environment.

For example, if our code relies on an external database, we can create a fake implementation that simulates the behavior of the database:

```python
class FakeDatabase:
    def __init__(self):
        self.data = {}

    def get(self, key):
        return self.data.get(key)

    def set(self, key, value):
        self.data[key] = value

# Usage
fake_db = FakeDatabase()
fake_db.set('key', 'value')
result = fake_db.get('key')
print(result)  # Output: 'value'
```

Fakes allow us to control the behavior of the dependency and provide predictable results during testing.

## Conclusion
Test doubles like mocks, stubs, and fakes are powerful tools in Python testing for isolating code from its dependencies. They enable us to create controlled environments where we can focus on testing specific functionality without worrying about the complexities of real systems.

By using these test doubles effectively, we can write comprehensive and reliable tests that improve the quality of our code.