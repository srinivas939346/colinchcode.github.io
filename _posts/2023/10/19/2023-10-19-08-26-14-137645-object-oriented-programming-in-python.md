---
layout: post
title: "[python] Object-oriented programming in Python"
description: " "
date: 2023-10-19
tags: [python]
comments: true
share: true
---

Object-oriented programming (OOP) is a programming paradigm that enables developers to model real-world objects as software objects. Python, being an object-oriented programming language, provides built-in support for creating and working with objects.

## What is an object?

In Python, an object is an instance of a class. A class serves as a blueprint for creating objects. It encapsulates data and provides methods to manipulate that data. Each object created from a class has its own unique set of data and can perform actions defined by the class methods.

## Defining a class

To define a class in Python, you use the `class` keyword followed by the class name. Let's create a simple class called `Car`:

```python
class Car:
    pass
```

This creates a basic class without any attributes or methods. The `pass` statement is used as a placeholder since Python requires an indented block after creating a class.

## Creating objects

Once we have defined a class, we can create objects (also known as instances) of that class. To create an object, simply call the class as if it were a function. For example:

```python
my_car = Car()
```

Here, `my_car` is an object of the `Car` class.

## Adding attributes

We can define attributes within a class to store data. These attributes represent the characteristics or properties of an object. To define attributes, we use the `__init__` method, also known as the constructor, within the class definition. 

```python
class Car:
    def __init__(self, brand, color):
        self.brand = brand
        self.color = color
```

In the above example, we have defined the `__init__` method that takes additional parameters for the brand and color of the car. We use the `self` parameter to refer to the object being created and assign the values to the object's attributes.

## Adding methods

Methods define the behavior or actions that objects can perform. They are defined within the class and are associated with objects created from that class.

```python
class Car:
    def __init__(self, brand, color):
        self.brand = brand
        self.color = color
    
    def start(self):
        print(f"The {self.color} {self.brand} car has started.")

    def stop(self):
        print(f"The {self.color} {self.brand} car has stopped.")
```

Here, we have defined two methods: `start()` and `stop()`. These methods print out a message indicating whether the car has started or stopped.

## Using objects and their methods

Once we have created objects of a class, we can use their attributes and call their methods. For example:

```python
my_car = Car("Toyota", "red")

print(f"My car is a {my_car.color} {my_car.brand}.")
my_car.start()
my_car.stop()
```

Output:
```
My car is a red Toyota.
The red Toyota car has started.
The red Toyota car has stopped.
```

In the above example, we create a `Car` object called `my_car` with the brand "Toyota" and color "red". We then access the object's attributes using dot notation and call its methods.

## Conclusion

Python's support for object-oriented programming allows developers to represent complex systems in an organized and modular way. By defining classes, creating objects, and defining their attributes and methods, we can build powerful and flexible programs that closely resemble the real world.

For more information on object-oriented programming in Python, refer to the official Python documentation: [Python OOP Documentation](https://docs.python.org/3/tutorial/classes.html)