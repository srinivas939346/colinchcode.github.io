---
layout: post
title: "[python] Astrodynamics simulation using Python"
description: " "
date: 2023-10-20
tags: [python]
comments: true
share: true
---

Astrodynamics is a branch of aerospace engineering that deals with the study of motion, position, and energy of objects in space. It involves the mathematical modeling and simulation of the dynamics of celestial bodies, such as planets, satellites, and asteroids.

Python, being a versatile and powerful language, can be used to simulate and analyze various astrodynamics problems. In this blog post, we will explore how to perform an astrodynamics simulation using Python.

## Installing Required Libraries

Before we start, let's make sure we have the necessary libraries installed. We will be using the `numpy` and `matplotlib` libraries for numerical computation and visualization, respectively. To install them, run the following commands:

```python
pip install numpy
pip install matplotlib
```

## Modeling Celestial Bodies

The first step in an astrodynamics simulation is to model the celestial bodies involved. We need to define their properties such as mass, position, velocity, and gravitational parameters.

Let's consider a simple scenario where we have a central celestial body (e.g., a planet) and a satellite orbiting around it. We can model the central body as a stationary point mass and the satellite as a point mass with its initial position and velocity.

```python
class CelestialBody:
    def __init__(self, mass):
        self.mass = mass

class Satellite:
    def __init__(self, mass, position, velocity):
        self.mass = mass
        self.position = position
        self.velocity = velocity
```

## Simulating the Motion

To simulate the motion of the satellite around the central body, we need to numerically integrate the equations of motion. The most commonly used method for this is the **Orbit Propagation** method.

Let's implement a simple function that simulates the motion of the satellite for a given time interval and step size.

```python
def simulate_motion(central_body, satellite, time_interval, step_size):
    time = 0
    positions = []
    velocities = []

    while time <= time_interval:
        # Compute the acceleration using gravitational force
        acceleration = compute_gravitational_acceleration(central_body, satellite)

        # Update the position and velocity
        satellite.position += satellite.velocity * step_size
        satellite.velocity += acceleration * step_size

        # Store the position and velocity
        positions.append(satellite.position)
        velocities.append(satellite.velocity)

        time += step_size

    return positions, velocities
```

## Computing the Gravitational Acceleration

To compute the gravitational acceleration acting on the satellite, we need to use Newton's law of universal gravitation. The gravitational force between two point masses can be calculated as follows:

```python
def compute_gravitational_acceleration(central_body, satellite):
    gravitational_constant = 6.67430e-11

    # Calculate the distance between the two bodies
    distance = numpy.linalg.norm(satellite.position - central_body.position)

    # Calculate the gravitational acceleration
    acceleration = gravitational_constant * central_body.mass / distance**2

    # Calculate the direction of the acceleration
    direction = (central_body.position - satellite.position) / distance

    return acceleration * direction
```

## Running the Simulation

Now that we have all the necessary components, let's run the simulation and visualize the results. We will simulate the motion of a satellite around a central body for a specific time interval and step size.

```python
import numpy as np
import matplotlib.pyplot as plt

# Define the central body and satellite
central_body = CelestialBody(5.972e24)  # Earth
satellite = Satellite(1000, np.array([10000, 0, 0]), np.array([0, 10000, 0]))

# Simulate the motion
time_interval = 1000  # seconds
step_size = 1  # seconds
positions, velocities = simulate_motion(central_body, satellite, time_interval, step_size)

# Visualize the results
plt.plot(positions)
plt.xlabel('Time')
plt.ylabel('Position')
plt.show()
```

## Conclusion

In this blog post, we have explored how to perform an astrodynamics simulation using Python. We learned how to model celestial bodies, simulate their motion, compute gravitational acceleration, and visualize the results using the `numpy` and `matplotlib` libraries.

Astrodynamics simulations are highly complex and involve many more factors than covered in this post. However, this basic implementation provides a starting point for further exploration and deeper understanding of astrodynamics.