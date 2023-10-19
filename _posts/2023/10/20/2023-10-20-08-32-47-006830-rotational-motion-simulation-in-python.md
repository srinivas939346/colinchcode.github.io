---
layout: post
title: "[python] Rotational motion simulation in Python"
description: " "
date: 2023-10-20
tags: [python]
comments: true
share: true
---

Rotational motion is an essential concept in physics and engineering. It involves the motion of objects around a fixed axis, such as a spinning top or a rotating wheel. In this blog post, we will explore how to simulate rotational motion using Python.

## Table of Contents

- [Introduction](#introduction)
- [Simulation Setup](#simulation-setup)
- [Simulating Rotational Motion](#simulating-rotational-motion)
- [Visualizing the Simulation](#visualizing-the-simulation)
- [Conclusion](#conclusion)

## Introduction
Rotational motion can be described using angular displacement, angular velocity, and angular acceleration. Angular displacement refers to the change in angle of an object, angular velocity represents the rate of change of angular displacement, and angular acceleration represents the rate of change of angular velocity.

Simulating rotational motion can help us understand how objects rotate and how different forces and torques impact their motion. Python is a versatile programming language and offers various libraries and tools that enable us to create simulations easily.

## Simulation Setup
To start with, we need to set up our simulation environment. We will be using the `numpy` library to perform vector calculations and the `matplotlib` library to visualize the simulation. If you don't have these libraries installed, you can install them using `pip`.

```python
import numpy as np
import matplotlib.pyplot as plt
```

## Simulating Rotational Motion
To simulate rotational motion, we need to define the properties of the rotating object. This includes its moment of inertia, angular velocity, and any forces or torques acting on it. 

Let's consider a simple example of a rotating disc. We can define its moment of inertia using the formula: 

*I = (1/2) * m * r^2*

where *m* is the mass of the disc and *r* is its radius.

To update the angular velocity of the disc, we need to consider any torques acting on it. Assuming no external torques, the change in angular velocity can be calculated using:

*delta_omega = (torque / I) * delta_t*

where *torque* is the net torque acting on the disc and *delta_t* is the time interval.

```python
def update_angular_velocity(angular_velocity, torque, moment_of_inertia, delta_t):
    delta_omega = (torque / moment_of_inertia) * delta_t
    return angular_velocity + delta_omega
```

We can use this function to update the angular velocity of our rotating disc at each time step.

## Visualizing the Simulation
To visualize the simulation, we can create a simple plot using `matplotlib`. We will assume that the rotating disc is initially at rest and has a constant torque acting on it.

```python
def simulate_rotational_motion(mass, radius, torque, time_interval, simulation_time):
    moment_of_inertia = (1/2) * mass * radius**2
    angular_velocity = 0
    time = np.arange(0, simulation_time, time_interval)
    angular_velocities = []

    for t in time:
        angular_velocity = update_angular_velocity(angular_velocity, torque, moment_of_inertia, time_interval)
        angular_velocities.append(angular_velocity)

    plt.plot(time, angular_velocities)
    plt.xlabel('Time')
    plt.ylabel('Angular Velocity')
    plt.title('Rotational Motion Simulation')
    plt.show()
```

We can call this function with appropriate parameters to simulate the rotational motion of our rotating disc and visualize the angular velocity over time.

## Conclusion
Simulating rotational motion in Python allows us to understand how objects rotate and how different forces and torques affect their motion. By using the `numpy` and `matplotlib` libraries, we can easily create simulations and visualize the results. This can be useful in various fields such as physics, engineering, and computer graphics.

Keep in mind that this is a simplified example, and actual simulations may require more complex calculations and considerations. However, with the knowledge and tools provided in this blog post, you can build upon this foundation to create more advanced simulations of rotational motion in Python.

References:
- [Numpy Documentation](https://numpy.org/doc/)
- [Matplotlib Documentation](https://matplotlib.org/stable/contents.html)