---
layout: post
title: "[python] Sending values to a generator in Python"
description: " "
date: 2023-10-18
tags: [python]
comments: true
share: true
---

Generators are a powerful feature in Python that allow us to iterate over a sequence of values without storing them all in memory. One useful feature of generators is the ability to send values back into them during iteration.

To send a value to a generator, we can use the `send()` method. Here's an example:

```python
def my_generator():
    value = yield  # The yield statement pauses the generator and returns a value
    print(f"Received value: {value}")
    value = yield value + 1
    print(f"Received value: {value}")

gen = my_generator()
next(gen)  # Advance to the first yield statement
gen.send(10)  # Send the value 10 to the generator
```

In the above code, `my_generator` is a generator function that yields values. We create an instance of the generator using `gen = my_generator()` and then advance it to the first yield statement using `next(gen)`. This prepares the generator for receiving a value.

We then use `gen.send(10)` to send the value `10` to the generator. This value is received by the generator and stored in the `value` variable. The generator then continues its execution and prints `Received value: 10`. It then encounters the next yield statement, which returns `value + 1` back to the caller.

If we want to send more values to the generator, we can simply call `gen.send()` again:

```python
next(gen)  # Advance to the second yield statement
gen.send(20)  # Send the value 20 to the generator
```

In this case, the generator will receive `20` as the new value and print `Received value: 20`. It will then continue its execution and return `value + 1`, which can be captured and used as desired.

It's important to note that the first call to `next(gen)` is necessary to prepare the generator for receiving values with `gen.send()`. If we don't call `next(gen)` before using `gen.send()`, a `TypeError` will be raised.

Generators are a powerful tool for managing sequences of values in a memory-efficient way, and the ability to send values back into them allows for even greater control and flexibility in our code.

References:
- [Python documentation - Generators](https://docs.python.org/3/tutorial/classes.html#generators)