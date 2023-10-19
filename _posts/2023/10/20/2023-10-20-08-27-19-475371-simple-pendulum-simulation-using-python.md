---
layout: post
title: "[python] Simple pendulum simulation using Python"
description: " "
date: 2023-10-20
tags: [python]
comments: true
share: true
---

In this blog post, we will explore how to simulate a simple pendulum using Python. A simple pendulum consists of a weight (bob) hanging from a string or rod, which is free to oscillate back and forth under the influence of gravity.

## Table of Contents
1. [Understanding simple pendulum motion](#understanding-simple-pendulum-motion)
2. [Simulating the pendulum motion](#simulating-the-pendulum-motion)
3. [Visualizing the simulation](#visualizing-the-simulation)
4. [Conclusion](#conclusion)

## Understanding simple pendulum motion

A simple pendulum is governed by the equation:

```
θ''(t) + (g / L) * sin(θ(t)) = 0
```

where `θ(t)` represents the angle of the pendulum at time `t`, `g` represents the acceleration due to gravity, and `L` represents the length of the pendulum.

This second-order ordinary differential equation describes the angular acceleration of the pendulum as a function of time. By numerically solving this equation, we can simulate the motion of the pendulum.

## Simulating the pendulum motion

To simulate the pendulum motion, we can utilize the numerical integration method. One popular method is the *Euler's Method*. We divide the time interval into small discrete steps and update the angular displacement and velocity of the pendulum at each step using the following equations:

```
θ(t + Δt) = θ(t) + ω(t) * Δt
ω(t + Δt) = ω(t) + (-g / L) * sin(θ(t)) * Δt
```

Here, `Δt` represents the time step, `θ(t)` represents the angle at time `t`, `ω(t)` represents the angular velocity at time `t`, `g` represents the acceleration due to gravity, and `L` represents the length of the pendulum.

Let's implement this simulation in Python:

```python
import math

def simulate_pendulum(theta0, omega0, length, g, delta_t, time):
    # Initialize the angular displacement and velocity
    theta = theta0
    omega = omega0

    # Simulate the pendulum motion
    for t in range(0, time, delta_t):
        theta_new = theta + omega * delta_t
        omega_new = omega + (-g / length) * math.sin(theta) * delta_t

        # Update the angular displacement and velocity
        theta = theta_new
        omega = omega_new

    return theta

# Example usage
theta0 = math.pi / 4  # Initial angle (in radians)
omega0 = 0.0  # Initial angular velocity (in radians per second)
length = 1.0  # Length of the pendulum (in meters)
g = 9.8  # Acceleration due to gravity (in meters per second squared)
delta_t = 0.01  # Time step (in seconds)
time = 10  # Total time (in seconds)

final_theta = simulate_pendulum(theta0, omega0, length, g, delta_t, time)
print(f"Final angle: {final_theta} radians")
```

In the above code, we define a function `simulate_pendulum` that takes initial angle, initial angular velocity, length, acceleration due to gravity, time step, and total time as input parameters. The function simulates the pendulum motion for the given time duration and returns the final angle.

## Visualizing the simulation

To visualize the pendulum simulation, we can utilize Python libraries like Matplotlib to plot the angle of the pendulum over time. Here's an example of how we can modify our simulation code to visualize the motion:

```python
import math
import matplotlib.pyplot as plt

def simulate_pendulum(theta0, omega0, length, g, delta_t, time):
    # Initialize the angular displacement and velocity
    theta = theta0
    omega = omega0

    # Track the angle over time
    angles = [theta]

    # Simulate the pendulum motion
    for t in range(0, time, delta_t):
        theta_new = theta + omega * delta_t
        omega_new = omega + (-g / length) * math.sin(theta) * delta_t

        # Update the angular displacement and velocity
        theta = theta_new
        omega = omega_new

        angles.append(theta)

    return angles

# Example usage
theta0 = math.pi / 4  # Initial angle (in radians)
omega0 = 0.0  # Initial angular velocity (in radians per second)
length = 1.0  # Length of the pendulum (in meters)
g = 9.8  # Acceleration due to gravity (in meters per second squared)
delta_t = 0.01  # Time step (in seconds)
time = 10  # Total time (in seconds)

angles = simulate_pendulum(theta0, omega0, length, g, delta_t, time)

# Plotting the angle over time
time_points = [t for t in range(0, time, delta_t)]
plt.plot(time_points, angles)
plt.xlabel('Time (seconds)')
plt.ylabel('Angle (radians)')
plt.title('Simple Pendulum Motion')
plt.show()
```

In the modified code, we track the angle of the pendulum over time by storing the angles in a list (`angles`). After simulating the motion, we plot the angles against time using the Matplotlib library.

## Conclusion

In this blog post, we explored how to simulate a simple pendulum using Python. By numerically solving the equation of motion and visualizing the results, we can gain insights into the behavior of a pendulum.

Simulations like these are valuable for understanding the dynamics of physical systems and can be used in various fields such as physics education, engineering, and robotics.