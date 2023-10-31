---
layout: post
title: "[python] MicroPython file handling and manipulation"
description: " "
date: 2023-10-31
tags: [python]
comments: true
share: true
---

MicroPython is a lightweight implementation of the Python programming language that is designed for microcontrollers and other constrained environments. It provides a subset of the standard Python language features and libraries, including file handling and manipulation functions. In this article, we will explore how to work with files in MicroPython.

## Table of Contents

1. [Opening a File](#opening-a-file)
2. [Reading from a File](#reading-from-a-file)
3. [Writing to a File](#writing-to-a-file)
4. [Closing a File](#closing-a-file)
5. [File Manipulation](#file-manipulation)

## Opening a File

To open a file in MicroPython, you can use the `open()` function. The function takes two arguments: the path to the file and the mode in which you want to open the file. The mode can be `'r'` for reading, `'w'` for writing, or `'a'` for appending.

```python
file = open('example.txt', 'r')
```

## Reading from a File

Once a file is opened for reading, you can use the `read()` method to read the contents of the file. This method returns a string containing the content.

```python
content = file.read()
print(content)
```

You can also read a specific number of characters from the file using the `read(n)` method, where `n` is the number of characters to read.

```python
partial_content = file.read(10)
print(partial_content)
```

## Writing to a File

When a file is opened for writing, you can use the `write()` method to write data to the file. This method takes a string as an argument.

```python
file = open('example.txt', 'w')
file.write("Hello, World!")
file.close()
```

If the file already exists, opening it in write mode will overwrite its contents. To append data to an existing file, open it in append mode (`'a'`) instead.

## Closing a File

After you finish working with a file, it is important to close it to free up system resources. You can close a file using the `close()` method.

```python
file.close()
```

## File Manipulation

MicroPython also provides several methods for file manipulation. These methods allow you to check if a file exists, rename or delete a file, and obtain information about a file.

Here are some examples:

```python
import os

# Check if a file exists
if os.path.exists('example.txt'):
    print("File exists")

# Rename a file
os.rename('example.txt', 'new_example.txt')

# Delete a file
os.remove('new_example.txt')

# Get file information
info = os.stat('example.txt')
print(info)
```

These file manipulation methods can be useful when working with files in MicroPython.

## Conclusion

MicroPython provides a simplified file handling and manipulation system that allows you to work with files on microcontrollers and other constrained devices. By understanding how to open files, read from them, write to them, and manipulate them, you can leverage the power of MicroPython to create applications that interact with files efficiently.

For more information, you can refer to the [MicroPython documentation](https://docs.micropython.org/en/latest/library/index.html).