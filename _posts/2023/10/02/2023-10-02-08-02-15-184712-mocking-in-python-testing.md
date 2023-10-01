---
layout: post
title: "[python] Mocking in Python testing"
description: " "
date: 2023-10-02
tags: [python]
comments: true
share: true
---

When writing unit tests in Python, it is often necessary to mock certain objects or functions to isolate the code being tested and control the behavior of dependencies. This allows us to test the code in isolation without relying on external resources or complex setups. In this blog post, we will explore the concept of mocking in Python testing and how it can be useful in different scenarios.

## Table of Contents
- [What is Mocking?](#what-is-mocking)
- [Using the `unittest.mock` Module](#using-the-unittestmock-module)
- [Creating a Mock Object](#creating-a-mock-object)
- [Mocking Functions](#mocking-functions)
- [Verifying Calls](#verifying-calls)
- [Mocking Exceptions](#mocking-exceptions)
- [Conclusion](#conclusion)

## What is Mocking?

**Mocking** is a technique used in software testing to replace a real object or function with a **dummy** object that mimics its behavior. This allows us to simulate the behavior of dependencies and control the output or side effects during testing.

By replacing real objects or functions with mock objects, we can isolate the code being tested and verify its behavior in different scenarios. Mocking can be particularly useful when testing code that relies on external services, databases, or expensive computations.

## Using the `unittest.mock` Module

Python provides a built-in module called `unittest.mock` (available as `mock` in Python 3.3+) that makes it easy to create and use mock objects in your tests. This module provides a wide range of functionalities for mocking objects, functions, and classes.

To use the `unittest.mock` module, you need to import it into your test module:

```python
from unittest.mock import MagicMock, Mock, patch
```