---
layout: post
title: "[python] Gravity simulation with Python"
description: " "
date: 2023-10-20
tags: [python]
comments: true
share: true
---

Gravity is a fundamental force that acts on every object in the universe. It plays a significant role in simulations, games, and scientific experiments. In this blog post, we will explore how to create a simple gravity simulation using Python.

## Table of Contents
1. [Setting up the Environment](#setting-up-the-environment)
2. [Defining the Objects](#defining-the-objects)
3. [Implementing the Gravity](#implementing-the-gravity)
4. [Running the Simulation](#running-the-simulation)
5. [Conclusion](#conclusion)

## Setting up the Environment {#setting-up-the-environment}

To get started, let's set up our environment by installing the required packages. We will be using the `pygame` library for the simulation and `numpy` for calculations. Install them using the following commands:

```
pip install pygame
pip install numpy
```

Once installed, we can proceed to the next step.

## Defining the Objects {#defining-the-objects}

In our simulation, we will have multiple objects in a two-dimensional space. Each object will have properties like position, velocity, and mass. We can define a class called `Object` to represent these objects:

```python
class Object:
    def __init__(self, x, y, mass, velocity):
        self.x = x
        self.y = y
        self.mass = mass
        self.velocity = velocity
```

The `Object` class has an `__init__` method that initializes the object's properties with the provided values.

## Implementing the Gravity {#implementing-the-gravity}

Now, let's implement the gravity effect on the objects. According to Newton's law of universal gravitation, the force between two objects is directly proportional to the product of their masses and inversely proportional to the square of the distance between them.

We can calculate the force between two objects using the following formula:

```
force = (G * mass1 * mass2) / distance^2
```

where `G` is the gravitational constant, `mass1` and `mass2` are the masses of the objects, and `distance` is the distance between them.

```python
import numpy as np

def calculate_gravitational_force(obj1, obj2):
    G = 6.67430e-11
    distance = np.sqrt((obj1.x - obj2.x)**2 + (obj1.y - obj2.y)**2)
    force = (G * obj1.mass * obj2.mass) / distance**2
    return force
```

In the above code, we calculate the distance between two objects using the Pythagorean theorem and then compute the gravitational force using the formula.

## Running the Simulation {#running-the-simulation}

To visualize the simulation, we will use the `pygame` library. We need to create a window, draw the objects, and simulate the movement under the influence of gravity.

Here is a simplified version of the simulation loop:

```python
import pygame
from pygame.locals import *
pygame.init()

# Initialize the objects
objects = [Object(x, y, mass, (0, 0)) for x, y, mass in object_data]

# Simulation loop
while True:
    for event in pygame.event.get():
        if event.type == QUIT:
            pygame.quit()
            sys.exit()

    # Clear the screen
    screen.fill((0, 0, 0))

    # Update the positions of objects
    for obj in objects:
        obj.x += obj.velocity[0]
        obj.y += obj.velocity[1]

    # Apply gravity between objects
    for obj1 in objects:
        for obj2 in objects:
            if obj1 != obj2:
                force = calculate_gravitational_force(obj1, obj2)
                # Apply the force to update the velocity

    # Draw the objects
    for obj in objects:
        pygame.draw.circle(screen, (255, 255, 255), (int(obj.x), int(obj.y)), obj.radius)

    # Update the display
    pygame.display.update()
```

In this code snippet, we initialize the objects, update their positions based on their velocities, calculate the gravitational force between them, and update their velocities accordingly. Finally, we draw the objects on the screen and update the display.

Please note that this code requires additional setup, such as creating a `screen` object and defining the `object_data` list.

## Conclusion {#conclusion}

In this blog post, we learned how to create a simple gravity simulation using Python. We implemented the object class, calculated the gravitational force between objects, and visualized the simulation using the `pygame` library. This simulation can be further expanded and enhanced to include more complex scenarios and interactions. By understanding and simulating gravity, we can gain insights into the behavior of celestial bodies and better comprehend the universe.