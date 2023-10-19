---
layout: post
title: "[python] Classes and objects in Python"
description: " "
date: 2023-10-19
tags: [python]
comments: true
share: true
---

In Python, classes are a way to define custom types that can hold data and perform functions. Objects, on the other hand, are instances of those classes. They represent specific instances of the class and can have their own unique data.

## Defining a Class

To define a class in Python, you can use the `class` keyword followed by the class name. The class definition can include attributes and methods.

```python
class Car:
    def __init__(self, make, model, year):
        self.make = make
        self.model = model
        self.year = year

    def start_engine(self):
        print(f"{self.make} {self.model} engine started.")

    def drive(self, distance):
        print(f"{self.make} {self.model} drove {distance} miles.")

```

In the example above, we define a `Car` class with three attributes: `make`, `model`, and `year`. The `__init__` method is a special method that is called when an object is created from the class. It initializes the attributes of the object. This method takes `self` as the first parameter, which refers to the instance itself.

We also have two additional methods in the class: `start_engine` and `drive`. These methods can be called on an instance of the `Car` class.

## Creating Objects

Once we define a class, we can create objects (instances) of that class using the class name followed by parentheses.

```python
my_car = Car("Toyota", "Camry", 2021)
```

In the code above, we create an object `my_car` of the `Car` class with the make "Toyota", model "Camry", and year 2021.

## Accessing Attributes and Calling Methods

To access the attributes of an object, we use dot notation.

```python
print(my_car.make)
print(my_car.model)
print(my_car.year)
```

The code above will output the values of the attributes of the `my_car` object.

To call a method on an object, we also use dot notation.

```python
my_car.start_engine()
my_car.drive(100)
```

The code above will call the `start_engine` and `drive` methods on the `my_car` object.

## Conclusion

Classes and objects are powerful concepts in Python that allow us to define custom types and work with instances of those types. By understanding how to define classes, create objects, and interact with attributes and methods, you can leverage the power of object-oriented programming in your Python projects.

To learn more about classes and objects in Python, you can refer to the official documentation:
- [Python Classes and Objects](https://docs.python.org/3/tutorial/classes.html)