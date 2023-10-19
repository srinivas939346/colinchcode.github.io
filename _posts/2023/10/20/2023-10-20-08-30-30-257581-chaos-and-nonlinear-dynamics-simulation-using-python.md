---
layout: post
title: "[python] Chaos and nonlinear dynamics simulation using Python"
description: " "
date: 2023-10-20
tags: [python]
comments: true
share: true
---

In this article, we will explore chaos and nonlinear dynamics simulations using Python. Chaos theory studies systems that exhibit complex and unpredictable behavior, even though they follow deterministic rules. Nonlinear dynamics, on the other hand, focuses on the study of systems where small changes in initial conditions can have a significant impact on the outcome.

## Table of Contents
1. [Introduction to Chaos Theory](#introduction)
2. [Introduction to Nonlinear Dynamics](#nonlinear-dynamics)
3. [Lorenz Attractor Simulation](#lorenz-attractor)
4. [Rössler Attractor Simulation](#rossler-attractor)
5. [Conclusion](#conclusion)

## Introduction to Chaos Theory<a name="introduction"></a>

Chaos theory, developed by mathematician Edward Lorenz, studies systems that are sensitive to initial conditions, meaning that small changes in the starting state of a system can lead to vastly different outputs. Chaotic systems often exhibit great complexity and irregularity, making them difficult to predict or control.

Nonlinear Dynamics is closely related to chaos theory and deals with the study of systems that do not follow linear relationships between inputs and outputs. In nonlinear systems, small changes in input can result in non-proportional changes in output.

## Introduction to Nonlinear Dynamics<a name="nonlinear-dynamics"></a>

Nonlinear dynamics is concerned with the study of systems that exhibit complex behavior due to their nonlinearity. These systems can be found in various fields, including physics, biology, economics, and engineering.

Nonlinear dynamic systems are often described by equations known as differential equations, which relate the change in a system's state to its current state and external influences. Solving these equations allows us to simulate and understand the behavior of nonlinear systems.

## Lorenz Attractor Simulation<a name="lorenz-attractor"></a>

The Lorenz attractor is a famous chaotic system that arises from a set of differential equations developed by meteorologist Edward Lorenz. It represents the behavior of a simplified model of atmospheric convection.

To simulate the Lorenz attractor in Python, we can use the `scipy` library:

```python
import numpy as np
from scipy.integrate import solve_ivp
import matplotlib.pyplot as plt

def lorenz(t, y):
    sigma = 10
    rho = 28
    beta = 8 / 3
    x, y, z = y
    dx_dt = sigma * (y - x)
    dy_dt = x * (rho - z) - y
    dz_dt = x * y - beta * z
    return [dx_dt, dy_dt, dz_dt]

y0 = [1, 1, 1]
t_span = [0, 50]
sol = solve_ivp(lorenz, t_span, y0, t_eval=np.linspace(t_span[0], t_span[1], 10000))

fig = plt.figure()
ax = fig.add_subplot(111, projection='3d')
ax.plot(sol.y[0], sol.y[1], sol.y[2])
ax.set_xlabel("X")
ax.set_ylabel("Y")
ax.set_zlabel("Z")
plt.show()
```

Running this code will produce a 3D plot representing the trajectory of the Lorenz attractor.

## Rössler Attractor Simulation<a name="rossler-attractor"></a>

The Rössler attractor is another famous chaotic system that was discovered by German biochemist Otto Rössler. It is a continuous, autonomous system of ordinary differential equations and is often used as a simplified model for chemical reactions.

To simulate the Rössler attractor in Python, we can modify the previous code as follows:

```python
import numpy as np
from scipy.integrate import solve_ivp
import matplotlib.pyplot as plt

def rossler(t, y):
    a = 0.2
    b = 0.2
    c = 5.7
    x, y, z = y
    dx_dt = -y - z
    dy_dt = x + a * y
    dz_dt = b + z * (x - c)
    return [dx_dt, dy_dt, dz_dt]

y0 = [1, 1, 1]
t_span = [0, 100]
sol = solve_ivp(rossler, t_span, y0, t_eval=np.linspace(t_span[0], t_span[1], 10000))

fig = plt.figure()
ax = fig.add_subplot(111, projection='3d')
ax.plot(sol.y[0], sol.y[1], sol.y[2])
ax.set_xlabel("X")
ax.set_ylabel("Y")
ax.set_zlabel("Z")
plt.show()
```

This code will generate a 3D plot illustrating the behavior of the Rössler attractor.

## Conclusion<a name="conclusion"></a>

In this article, we explored chaos theory and nonlinear dynamics simulations using Python. We learned about the unpredictable behavior of chaotic systems and how small changes in initial conditions can affect their outcomes. We also simulated the Lorenz attractor and the Rössler attractor to visualize the complex behavior of these chaotic systems.

Chaos theory and nonlinear dynamics have many applications in various fields, and Python provides powerful libraries like `scipy` and `matplotlib` to simulate and visualize these systems. By studying chaotic systems, we can gain a deeper understanding of the complex phenomena observed in the world around us.

## References

- Lorenz attractor: https://en.wikipedia.org/wiki/Lorenz_system
- Rössler attractor: https://en.wikipedia.org/wiki/R%C3%B6ssler_attractor
- Scipy: https://docs.scipy.org/doc/scipy/reference/
- Matplotlib: https://matplotlib.org/stable/index.html