---
layout: post
title: "[python] Automated testing in Python using Selenium"
description: " "
date: 2023-10-02
tags: [python]
comments: true
share: true
---

## Introduction

Automated testing is a crucial part of the software development process. It helps ensure that the software is working as expected and prevents regression bugs. Selenium is a popular tool for automating web browsers, and Python provides a powerful framework for writing automated tests.

In this tutorial, we will explore how to perform automated testing in Python using Selenium.

## Prerequisites

Before we start, make sure you have the following:

- Python installed on your machine
- Selenium library installed (`pip install selenium`)
- A web browser (Chrome, Firefox, etc.) installed

## Setting up Selenium

To use Selenium in Python, we need to import the `webdriver` module and create an instance of the desired browser.

```python
from selenium import webdriver

driver = webdriver.Chrome()
```

In the code snippet above, we are using Chrome as the browser. However, you can use other browsers by simply changing `webdriver.Chrome()` to `webdriver.Firefox()`, `webdriver.Safari()`, etc.

## Writing our first test

Let's write a simple test to open a webpage and check the page title.

```python
from selenium import webdriver

driver = webdriver.Chrome()
driver.get("https://www.example.com")

expected_title = "Example Domain"
actual_title = driver.title

assert expected_title == actual_title

print("Test successfully passed!")

driver.quit()
```

In the code above, we first import the `webdriver` module and create an instance of Chrome. We then navigate to the website using the `get()` method. We retrieve the page title using the `title` attribute and compare it to the expected title. If they match, the test passes, and we print a success message. Finally, we close the browser using the `quit()` method.

## Locating elements

Automated tests often involve interacting with elements on a web page, like clicking buttons, filling forms, and extracting data. Selenium provides various methods to locate these elements.

- **By ID**:

  ```python
  element = driver.find_element_by_id("element_id")
  ```

- **By Name**:

  ```python
  element = driver.find_element_by_name("element_name")
  ```

- **By XPath**:

  ```python
  element = driver.find_element_by_xpath("//xpath_expression")
  ```

- **By CSS Selector**:

  ```python
  element = driver.find_element_by_css_selector("css_selector")
  ```

Once we have located an element, we can perform actions on it, such as clicking, typing, or extracting information.

## Running tests in headless mode

By default, Selenium opens a browser window when running tests. However, in some cases, we may want the tests to run in the background without any visible window. This is known as running tests in headless mode.

To run tests in headless mode, we can set the `headless` option to `True`:

```python
from selenium.webdriver.chrome.options import Options

options = Options()
options.headless = True

driver = webdriver.Chrome(options=options)
```

## Conclusion

In this tutorial, we explored how to perform automated testing in Python using Selenium. We learned how to set up Selenium, write tests, locate elements, and run tests in headless mode. Automated testing with Selenium is a powerful approach to ensure the quality and reliability of web applications.