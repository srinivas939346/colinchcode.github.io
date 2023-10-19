---
layout: post
title: "[python] Solar system simulation using Python"
description: " "
date: 2023-10-20
tags: [python]
comments: true
share: true
---

## Introduction

The study of celestial objects and their interactions has always fascinated scientists and astronomers. One way to understand these interactions is through the use of computer simulations. In this blog post, we will explore how to simulate the movement of celestial bodies in the solar system using Python.

## Requirements

To run this simulation, you will need to install the following Python libraries:

1. `matplotlib` - for creating visualizations
2. `numpy` - for mathematical calculations

You can install these libraries using the `pip` package manager by running the following command:

```
pip install matplotlib numpy
```

## Simulating Celestial Bodies

We will start by defining a `CelestialBody` class that represents a celestial object such as a planet or a moon. Each celestial body has properties like its mass, position, velocity, and acceleration. We will also define methods to update the position and velocity of the celestial body based on the gravitational forces acting on it.

```python
class CelestialBody:
    def __init__(self, mass, position, velocity):
        self.mass = mass
        self.position = np.array(position)
        self.velocity = np.array(velocity)
        self.acceleration = np.zeros(3)

    def update(self, force, dt):
        self.acceleration = force / self.mass
        self.velocity += self.acceleration * dt
        self.position += self.velocity * dt
```

We will also define a `SolarSystem` class that will hold a list of celestial bodies and provide methods to update their positions at each time step.

```python
class SolarSystem:
    def __init__(self):
        self.bodies = []

    def add_body(self, celestial_body):
        self.bodies.append(celestial_body)

    def update(self, dt):
        for body in self.bodies:
            total_force = np.zeros(3)
            for other_body in self.bodies:
                if other_body != body:
                    displacement = other_body.position - body.position
                    distance = np.linalg.norm(displacement)
                    force = (displacement / distance) * G * other_body.mass * body.mass / distance ** 2
                    total_force += force
            body.update(total_force, dt)
```

## Visualization

To visualize the simulation, we will use the `matplotlib` library. We can create a simple 3D scatter plot to represent the positions of the celestial bodies at each time step.

```python
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

def visualize_system(system):
    fig = plt.figure()
    ax = fig.add_subplot(111, projection='3d')
    for body in system.bodies:
        ax.scatter(body.position[0], body.position[1], body.position[2])
    plt.show()
```

## Running the Simulation

To test our simulation, let's create a solar system with the Sun, Earth, and Moon.

```python
G = 6.67430e-11

# Create celestial bodies
sun = CelestialBody(1.989e30, [0, 0, 0], [0, 0, 0])
earth = CelestialBody(5.972e24, [147e9, 0, 0], [0, 29.29e3, 0])
moon = CelestialBody(7.348e22, [147e9 + 384400e3, 0, 0], [0, 29.29e3 + 1.022e3, 0])

# Create solar system
system = SolarSystem()
system.add_body(sun)
system.add_body(earth)
system.add_body(moon)

# Run simulation
dt = 3600  # Time step in seconds
num_steps = 24 * 365  # Number of time steps

for _ in range(num_steps):
    system.update(dt)

visualize_system(system)
```

When you run the above code, you should see a 3D plot showing the positions of the Sun, Earth, and Moon at each time step.

## Conclusion

In this blog post, we have explored how to simulate the movement of celestial bodies in the solar system using Python. We have seen how to define a `CelestialBody` class to represent celestial objects and a `SolarSystem` class to manage the simulation. We have also used the `matplotlib` library to visualize the positions of the celestial bodies in the simulation.

Simulations like these can help us better understand the complex dynamics of celestial objects and can be used to study phenomena like planetary orbits and eclipses. Python provides us with powerful tools to perform such simulations, making it easier for scientists and astronomers to explore the mysteries of the universe.

## References

- [The Python Package Index (PyPI)](https://pypi.org/)
- [matplotlib documentation](https://matplotlib.org/stable/index.html)
- [numpy documentation](https://numpy.org/doc/)