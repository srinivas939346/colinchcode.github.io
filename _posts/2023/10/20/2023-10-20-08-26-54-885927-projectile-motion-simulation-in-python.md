---
layout: post
title: "[python] Projectile motion simulation in Python"
description: " "
date: 2023-10-20
tags: [python]
comments: true
share: true
---

In this blog post, we will discuss how to simulate projectile motion using Python. Projectile motion is the motion of an object that is launched into the air and moves along a curved path under the influence of gravity.

To simulate projectile motion, we need to take into account the initial velocity, launch angle, and the acceleration due to gravity. Using these parameters, we can calculate the position of the projectile at different points in time.

## The math behind projectile motion

Before diving into the simulation, let's briefly discuss the math behind projectile motion. The horizontal and vertical components of the projectile's motion can be calculated using the following equations:

Horizontal velocity (Vx) = initial velocity (Vo) * cos(angle)
Vertical velocity (Vy) = initial velocity (Vo) * sin(angle)

The horizontal position (x) and vertical position (y) of the projectile at a given time (t) are given by the equations:

x = Vx * t
y = Vy * t - 0.5 * gravity * t^2

where gravity is the acceleration due to gravity (9.8 m/s^2).

## Simulating projectile motion in Python

Let's now implement a simple projectile motion simulation in Python. We will use the `matplotlib` library to visualize the trajectory of the projectile.

```python
import matplotlib.pyplot as plt
import numpy as np

def projectile_simulation(initial_velocity, launch_angle):
    gravity = 9.8
    
    # Calculate the initial velocities
    Vx = initial_velocity * np.cos(np.deg2rad(launch_angle))
    Vy = initial_velocity * np.sin(np.deg2rad(launch_angle))

    # Calculate the time of flight
    time_of_flight = 2 * Vy / gravity

    # Create an array of time values
    t = np.linspace(0, time_of_flight, num=100)

    # Calculate the horizontal and vertical positions
    x = Vx * t
    y = Vy * t - 0.5 * gravity * t**2

    # Plot the trajectory
    plt.plot(x, y)
    plt.xlabel('Horizontal position (m)')
    plt.ylabel('Vertical position (m)')
    plt.title('Projectile Motion')
    plt.grid()
    plt.show()

# Run the simulation with initial velocity of 50 m/s and launch angle of 45 degrees
projectile_simulation(50, 45)
```

Running this code will generate a plot showing the trajectory of the projectile.

## Conclusion

Simulating projectile motion using Python allows us to analyze and visualize the motion of objects in the air. By understanding the math behind projectile motion, we can accurately model and predict the trajectory of a projectile. This knowledge has applications in fields such as physics, engineering, and game development.

Keep in mind that this is a basic implementation, and there are more advanced techniques that can be used to simulate more complex scenarios. Remember to always experiment and explore different approaches to gain a deeper understanding of the topic.

References:
- [Matplotlib documentation](https://matplotlib.org/)
- [NumPy documentation](https://numpy.org/)