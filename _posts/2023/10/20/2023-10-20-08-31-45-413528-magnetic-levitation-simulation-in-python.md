---
layout: post
title: "[python] Magnetic levitation simulation in Python"
description: " "
date: 2023-10-20
tags: [python]
comments: true
share: true
---

In this post, we will explore how to simulate magnetic levitation using Python. Magnetic levitation is a phenomenon where an object is suspended in the air against gravity, using the force of magnetic repulsion or attraction.

## Table of Contents
- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Simulation Setup](#simulation-setup)
- [Simulation Algorithm](#simulation-algorithm)
- [Results and Analysis](#results-and-analysis)
- [Conclusion](#conclusion)
- [References](#references)

## Introduction

Magnetic levitation has various applications in industries such as transportation, robotics, and energy storage. Simulating magnetic levitation can help us understand the underlying principles and dynamics involved in this phenomenon.

## Prerequisites

Before we get started with the simulation, we need to make sure Python is installed on our system. Additionally, we will need the `numpy` and `matplotlib` libraries for numerical computations and visualization.

To install these libraries, we can use the following commands:

```python
pip install numpy
pip install matplotlib
```

## Simulation Setup

To simulate magnetic levitation, we need to define the parameters of the system, such as the magnetic field, the magnetic properties of the levitating object, and the gravitational force.

Let's start by importing the required libraries and defining some constants:

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
g = 9.81          # Acceleration due to gravity (m/s^2)
mu_0 = 4 * np.pi * 1e-7   # Vacuum permeability (Tm/A)
```

Next, we can define the properties of the magnet and the levitating object:

```python
# Magnet properties
magnet_strength = 1     # Strength of the magnet (T)
magnet_position = np.array([0, 0, 0])   # Position of the magnet (m)

# Levitating object properties
object_mass = 0.1    # Mass of the object (kg)
object_charge = 0.1    # Charge of the object (C)
object_position = np.array([0, 0, 0.1])   # Initial position of the object (m)
object_velocity = np.array([0, 0, 0])   # Initial velocity of the object (m/s)
```

## Simulation Algorithm

To simulate the magnetic levitation, we can use a numerical integration method, such as the Euler method. This method approximates the position and velocity of the object at each time step.

Here's a basic implementation of the simulation algorithm:

```python
# Simulation parameters
t_start = 0     # Start time (s)
t_end = 10     # End time (s)
dt = 0.01     # Time step (s)

# Simulation
t = t_start
while t <= t_end:
    # Calculate the magnetic force
    magnetic_force = # Calculate the magnetic force using the object's position, magnet's position, and their properties
    
    # Calculate the gravitational force
    gravitational_force = np.array([0, 0, -object_mass * g])
    
    # Calculate the net force
    net_force = magnetic_force + gravitational_force
    
    # Update the object's position and velocity
    object_velocity += net_force / object_mass * dt
    object_position += object_velocity * dt
    
    # Update the time
    t += dt
```

## Results and Analysis

After running the simulation, we can plot the object's trajectory using the `matplotlib` library:

```python
# Plotting the trajectory
fig = plt.figure()
ax = fig.add_subplot(111, projection='3d')
ax.plot(object_position[:, 0], object_position[:, 1], object_position[:, 2])
ax.set_xlabel('X')
ax.set_ylabel('Y')
ax.set_zlabel('Z')
plt.show()
```

The resulting plot will show the path of the levitating object over time.

## Conclusion

In this post, we have learned how to simulate magnetic levitation using Python. By implementing the simulation algorithm, we can study the dynamics of magnetic levitation and explore its various real-world applications.

## References

1. Magnetic levitation - [Wikipedia](https://en.wikipedia.org/wiki/Magnetic_levitation)
2. Numpy library - [NumPy Documentation](https://numpy.org/doc/)
3. Matplotlib library - [Matplotlib Documentation](https://matplotlib.org/stable/contents.html)