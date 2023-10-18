---
layout: post
title: "[python] Lazy loading data using generators in Python"
description: " "
date: 2023-10-18
tags: [python]
comments: true
share: true
---

In Python, generators are a powerful tool for lazy loading and manipulating data. Unlike lists or other iterable objects, generators produce values on the fly as they are requested, instead of storing all the values in memory at once. This makes generators a great choice when dealing with large datasets or when we want to save memory.

## Creating a generator function

To create a generator, we use a special type of function called a "generator function". A generator function is defined like a regular function, but it uses the `yield` keyword instead of `return` to produce a series of values.

Here's an example of a simple generator function that generates a sequence of numbers:

```python
def number_generator(n):
    for i in range(n):
        yield i
```

In the above code, the `number_generator` function generates numbers from `0` to `n-1` using the `yield` keyword. When a value is yielded, the function pauses its execution and saves its state. The next time the generator is called, it resumes from where it left off.

## Using the generator

To use the generator we created, we can simply iterate over it using a `for` loop or by calling the `next()` function on it.

```python
gen = number_generator(5)

for num in gen:
    print(num)

# Output:
# 0
# 1
# 2
# 3
# 4
```

In the above code, we create an instance of the generator using `number_generator(5)`. We then iterate over the generator object using a `for` loop, which will yield each number one by one until the generator is exhausted.

Alternatively, we can use the `next()` function to get the next value from the generator:

```python
gen = number_generator(3)

print(next(gen))  # Output: 0
print(next(gen))  # Output: 1
print(next(gen))  # Output: 2
```

## Lazy loading data

One of the main benefits of using generators is the ability to lazy load data. This means that values are generated on-the-fly as they are needed, instead of loading all the data into memory at once.

Let's say we have a large dataset stored in a file. Instead of reading the entire file into memory, we can use a generator to read and process the data line by line.

```python
def process_data(file_path):
    with open(file_path, 'r') as file:
        for line in file:
            # Process the line here
            yield line.strip()
```

In the above code, the `process_data` generator reads the file line by line and `yield`s each line after performing any necessary processing. This way, we only load one line into memory at a time, allowing us to handle large datasets efficiently.

## Conclusion

Generators are a powerful tool in Python for lazy loading and manipulating data. They allow us to generate values on-the-fly, saving memory and improving performance, especially when dealing with large datasets. So next time you have to process a large amount of data, consider using generators to make your code more efficient.