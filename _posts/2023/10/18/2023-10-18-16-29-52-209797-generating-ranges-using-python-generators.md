---
layout: post
title: "[python] Generating ranges using Python generators"
description: " "
date: 2023-10-18
tags: [python]
comments: true
share: true
---

In Python, the `range` function is commonly used to generate a sequence of numbers. However, if you need more flexibility in generating ranges, you can utilize Python generators.

Generators are functions that can suspend and resume their execution, allowing you to create sequences on the fly without the need to store the entire range in memory. This can be especially useful when dealing with large ranges or infinite sequences.

Let's explore how to generate ranges using Python generators:

## Custom range generator

```python
def custom_range(start, stop, step=1):
    current = start
    while current < stop:
        yield current
        current += step
```

The `custom_range` function takes three arguments - `start`, `stop`, and optional `step`. It initializes a variable `current` with the starting value and continuously yields the current value while incrementing it by the step size.

## Generating a range using the custom generator

```python
my_range = custom_range(1, 10, 2)

for num in my_range:
    print(num)
```

In this example, we create a range generator `my_range` that starts from 1, ends at 10 (exclusive), and increments by 2. We then iterate over the generated sequence using a `for` loop and print each number.

## Benefits of using generator-based ranges

- **Memory efficiency**: Unlike the `range` function, which generates the entire range upfront, generator-based ranges generate values on-the-fly. This makes them memory-efficient as they only store the current value and not the entire sequence.
- **Flexibility**: With a custom range generator, you have more control over the generated sequence. You can define custom step sizes, generate infinite sequences, or even create ranges based on complex logic.
- **Lazy evaluation**: Generators have the advantage of lazy evaluation. The range generation stops as soon as it reaches the stop condition, allowing you to work with large ranges or infinite sequences without running out of memory.
- **Reusability**: Since generators are functions, you can create reusable ranges by defining them once and calling them whenever needed.

## Conclusion

Python generators provide a flexible and memory-efficient way to generate ranges. By utilizing generator-based ranges, you can create custom sequences on the fly and work with large ranges or infinite sequences without running into memory constraints. This enables you to write more efficient and scalable code.