---
layout: post
title: "[python] Planetary motion simulation with Python"
description: " "
date: 2023-10-20
tags: [python]
comments: true
share: true
---

In this blog post, we will explore how to simulate planetary motion using Python. We will use the laws of gravitation to model the motion of planets around a central star.

## Table of Contents
1. [Introduction](#introduction)
2. [The Laws of Gravitation](#laws-of-gravitation)
3. [Simulating Planetary Motion](#simulating-planetary-motion)
4. [Visualizing the Results](#visualizing-the-results)
5. [Conclusion](#conclusion)

## Introduction <a name="introduction"></a>

Understanding planetary motion is crucial in various fields such as astronomy and astrophysics. The laws of gravitation as formulated by Sir Isaac Newton provide a mathematical framework for explaining the motion of celestial bodies.

In this simulation, we will consider a simplified scenario with a central star and a single planet. This will allow us to focus on the basics of planetary motion.

## The Laws of Gravitation <a name="laws-of-gravitation"></a>

According to Newton's law of gravitation, the force between two bodies is directly proportional to the product of their masses and inversely proportional to the square of the distance between them. Mathematically, it can be expressed as:

F = G * (m1 * m2) / r^2

where F is the force, G is the gravitational constant, m1 and m2 are the masses of the two bodies, and r is the distance between them.

## Simulating Planetary Motion <a name="simulating-planetary-motion"></a>

To simulate planetary motion, we need to consider the gravitational force acting on the planet from the star. By applying Newton's laws of motion, we can determine the acceleration of the planet. With this information, we can update the position and velocity of the planet at each time step.

Here's an example code snippet in Python that demonstrates the simulation:

```python
import numpy as np

def simulate_planetary_motion(mass_star, mass_planet, initial_position, initial_velocity, time_step, num_steps):
    G = 6.67430e-11  # gravitational constant

    positions = np.zeros((num_steps, 2))
    velocities = np.zeros((num_steps, 2))

    positions[0] = initial_position
    velocities[0] = initial_velocity

    for i in range(1, num_steps):
        distance = np.linalg.norm(positions[i-1])  # distance to the star
        acceleration = -G * mass_star * positions[i-1] / distance**3  # acceleration due to gravity

        positions[i] = positions[i-1] + velocities[i-1] * time_step
        velocities[i] = velocities[i-1] + acceleration * time_step

    return positions, velocities
```

In this code, we use the `numpy` library to handle vector calculations efficiently. The `simulate_planetary_motion` function takes the masses of the star and the planet, the initial position and velocity of the planet, the time step, and the number of steps to simulate. It returns the positions and velocities of the planet at each time step.

## Visualizing the Results <a name="visualizing-the-results"></a>

To visualize the simulated planetary motion, we can use a library like `matplotlib`. By plotting the positions of the planet over time, we can observe its orbit around the star.

Here's an example code snippet that demonstrates how to plot the results:

```python
import matplotlib.pyplot as plt

def plot_planetary_motion(positions):
    plt.figure(figsize=(6, 6))
    plt.plot(positions[:, 0], positions[:, 1])
    plt.scatter(0, 0, c='yellow', label='Star')
    plt.scatter(positions[0, 0], positions[0, 1], c='blue', label='Planet (initial)')
    plt.scatter(positions[-1, 0], positions[-1, 1], c='red', label='Planet (final)')
    plt.xlabel('X')
    plt.ylabel('Y')
    plt.title('Planetary Motion')
    plt.legend()
    plt.show()
```

This code snippet creates a scatter plot of the positions and adds markers for the star, initial planet position, and final planet position.

## Conclusion <a name="conclusion"></a>

Simulating planetary motion using Python allows us to understand and visualize the dynamics of celestial bodies. By leveraging the laws of gravitation and numerical methods, we can model complex scenarios involving multiple planets and stars. This paves the way for further exploration and analysis in the field of astronomy and astrophysics.

References:
- [Laws of gravitation - Wikipedia](https://en.wikipedia.org/wiki/Newton%27s_laws_of_motion)
- [NumPy Documentation](https://numpy.org/doc/stable/)
- [Matplotlib Documentation](https://matplotlib.org/stable/contents.html)