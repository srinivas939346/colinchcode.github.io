---
layout: post
title: "[python] Lookahead and lookbehind assertions in regular expressions"
description: " "
date: 2023-09-29
tags: [python]
comments: true
share: true
---

Regular expressions are a powerful tool for pattern matching and extracting information from strings. They allow you to search for specific patterns in a text by defining a certain set of rules.

In this article, we'll explore lookahead and lookbehind assertions in regular expressions. These assertions allow you to check for patterns that are either followed by or preceded by another pattern, without including it in the matched result.

## Lookahead Assertions

Lookahead assertions, denoted by a question mark followed by an equal sign (`?=pattern`), are used to assert that a particular pattern must be **present** after the current position in the string.

For example, let's say we want to find all instances of the word "apple" that are followed by the word "pie". We can use the lookahead assertion to accomplish this:

```python
import re

text = "I love apple pie, but not apple juice."
result = re.findall(r"apple(?= pie)", text)

print(result)
```

Output:
```
['apple']
```

In the code snippet above, we use the `re.findall()` function to find all occurrences of the word "apple" that are followed by "pie". Since "apple" is immediately followed by " pie" in the string, it matches the given pattern and is included in the result.

## Lookbehind Assertions

Similarly, lookbehind assertions, denoted by a question mark followed by a less than sign (`?<=pattern`), are used to assert that a particular pattern must be **preceded** by the current position in the string.

Let's consider another example where we want to find all instances of the word "pie" that are preceded by the word "apple". Here's how we can use the lookbehind assertion in Python:

```python
import re

text = "I love apple pie, but not apple juice."
result = re.findall(r"(?<=apple )pie", text)

print(result)
```

Output:
```
['pie']
```

In the code snippet above, we use the `re.findall()` function with the pattern `(?<=apple )pie`. This pattern matches the word "pie" only if it is preceded by the word "apple" and a space. As a result, the output includes the word "pie".

## Lookaround Assertions

Lookahead and lookbehind assertions can also be combined to perform more complex pattern matching. This is known as lookaround assertions or simply lookahead/lookbehind combinations.

For example, let's say we want to find all instances of the word "apple" that are both preceded by the word "I love" and followed by the word "pie". Here's how we can achieve this using lookaround assertions:

```python
import re

text = "I love apple pie, but not apple juice."
result = re.findall(r"(?<=I love )apple(?= pie)", text)

print(result)
```

Output:
```
['apple']
```

In the code snippet above, we use `(?<=I love )` as the lookbehind assertion to match the word "apple" only if it is preceded by the phrase "I love". Similarly, we use `(?= pie)` as the lookahead assertion to match the word "apple" only if it is followed by the word "pie". As a result, only the word "apple" that satisfies both conditions is included in the output.

## Conclusion

Lookahead and lookbehind assertions provide an additional level of control and flexibility when using regular expressions. They allow you to define complex patterns by specifying conditions that must be met before or after a particular pattern. By utilizing these features, you can perform more advanced string matching and extraction operations in Python.