---
layout: post
title: "[python] Friction simulation in Python"
description: " "
date: 2023-10-20
tags: [python]
comments: true
share: true
---

In this blog post, we will explore how to simulate friction using Python. Friction is a force that opposes the motion of objects in contact with each other, and it plays a crucial role in various physical simulations.

Friction can be simulated using numerical methods, such as the Euler method, which approximates the motion of objects over time. We will demonstrate this method by creating a simple simulation of a box sliding on a surface with friction.

## Table of Contents
1. [Setting up the Environment](#setting-up-the-environment)
2. [Defining the Dynamics](#defining-the-dynamics)
3. [Implementing the Euler Method](#implementing-the-euler-method)
4. [Simulating Friction](#simulating-friction)
5. [Conclusion](#conclusion)

## Setting up the Environment

To begin, we need to set up our Python environment. We will be using the `numpy` library for numerical calculations, so make sure to install it if you haven't already.

```python
!pip install numpy
```

Once `numpy` is installed, import it along with any other necessary libraries:

```python
import numpy as np
import matplotlib.pyplot as plt
```

## Defining the Dynamics

In our simulation, we will consider a box of mass `m` sliding on a surface with friction. The box experiences a gravitational force and a frictional force opposing its motion. We can define the dynamics of the box using the following equations:

```python
m = 1  # mass of the box
g = 9.8  # gravitational acceleration

def acceleration(friction):
    return -g + friction / m

def velocity(friction, dt):
    return friction / m * dt

def displacement(velocity, dt):
    return velocity * dt
```

## Implementing the Euler Method

Now, we can implement the Euler method to approximate the motion of the box over time. The Euler method uses discrete steps to update the velocity and position of the box based on the acceleration at each step.

```python
def euler(friction, dt, steps):
    velocities = [0]
    positions = [0]

    for step in range(steps):
        vel = velocities[-1] + acceleration(friction) * dt
        pos = positions[-1] + velocity(friction, dt) * dt

        velocities.append(vel)
        positions.append(pos)

    return velocities, positions
``` 

## Simulating Friction

To simulate friction, we need to specify the frictional force acting on the box. This can be done based on the properties of the surfaces in contact. For simplicity, let's assume a constant coefficient of friction `mu`.

```python
mu = 0.2  # coefficient of friction

def frictional_force(vel):
    return -mu * m * g * np.sign(vel)
```

Now, let's put it all together and run our simulation.

```python
friction = frictional_force(0.5)  # initial velocity of the box
dt = 0.1  # time step
steps = 100  # number of steps

velocities, positions = euler(friction, dt, steps)

plt.plot(positions)
plt.xlabel('Time')
plt.ylabel('Position')
plt.show()
```

## Conclusion

In this blog post, we learned how to simulate friction using the Euler method in Python. By approximating the motion of objects over time, we can study the effects of friction in various scenarios. This simulation can be extended to include more complex dynamics or multiple objects interacting with each other.