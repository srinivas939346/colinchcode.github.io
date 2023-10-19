---
layout: post
title: "[python] Oscillations and resonance simulation in Python"
description: " "
date: 2023-10-20
tags: [python]
comments: true
share: true
---

In this tutorial, we will explore how to simulate oscillations and resonance using Python. Oscillations are repetitive movements or fluctuations around an equilibrium point, while resonance occurs when an oscillating system is driven at its natural frequency, resulting in a significantly amplified response. Understanding these concepts can be useful in various fields such as physics, engineering, and signal processing.

To perform this simulation, we will be using the `numpy` and `matplotlib` libraries in Python. So make sure you have them installed before proceeding. If not, you can install them using `pip`:

```
pip install numpy matplotlib
```

### Simple Harmonic Motion

Let's start by simulating simple harmonic motion, which is a type of oscillation that is governed by Hooke's Law. The equation for simple harmonic motion is:

```python
F = -k * x
```

where `F` is the restoring force, `k` is the spring constant, and `x` is the displacement from the equilibrium position.

We can simulate simple harmonic motion by numerically solving the differential equation that describes it. Here's an example code that simulates and plots the motion:

```python
import numpy as np
import matplotlib.pyplot as plt

def simulate_simple_harmonic_motion(k, x0, v0, dt, num_steps):
    t = np.linspace(0, (num_steps - 1) * dt, num=num_steps)
    x = np.zeros(num_steps)
    v = np.zeros(num_steps)
  
    x[0] = x0
    v[0] = v0
  
    for i in range(1, num_steps):
        F = -k * x[i - 1]
        a = F / m
  
        x[i] = x[i - 1] + v[i - 1] * dt
        v[i] = v[i - 1] + a * dt

    return t, x

# Simulation parameters
k = 1.0
x0 = 1.0
v0 = 0.0
dt = 0.01
num_steps = 1000

# Simulate and plot simple harmonic motion
t, x = simulate_simple_harmonic_motion(k, x0, v0, dt, num_steps)
plt.plot(t, x)
plt.xlabel('Time')
plt.ylabel('Displacement')
plt.title('Simple Harmonic Motion')
plt.show()
```

By changing the values of the simulation parameters, you can explore different types of simple harmonic motion.

### Resonance

Now, let's move on to simulating resonance. Resonance occurs when an oscillating system is subjected to an external force at its natural frequency. This leads to a large amplitude response, which can result in destructive or constructive interference.

To simulate resonance, we can extend our previous code by introducing an external force `F_ext(t)` that drives the system at its natural frequency. Here's an example code that simulates and plots the resonance:

```python
import numpy as np
import matplotlib.pyplot as plt

def simulate_resonance(k, x0, v0, F_ext, dt, num_steps):
    t = np.linspace(0, (num_steps - 1) * dt, num=num_steps)
    x = np.zeros(num_steps)
    v = np.zeros(num_steps)
  
    x[0] = x0
    v[0] = v0
  
    for i in range(1, num_steps):
        F = -k * x[i - 1] + F_ext(t[i])
        a = F / m
  
        x[i] = x[i - 1] + v[i - 1] * dt
        v[i] = v[i - 1] + a * dt

    return t, x

# Simulation parameters
k = 1.0
x0 = 1.0
v0 = 0.0
dt = 0.01
num_steps = 1000

# External force function
def F_ext(t):
    return np.sin(2 * np.pi * t)

# Simulate and plot resonance
t, x = simulate_resonance(k, x0, v0, F_ext, dt, num_steps)
plt.plot(t, x)
plt.xlabel('Time')
plt.ylabel('Displacement')
plt.title('Resonance')
plt.show()
```

In this example, `F_ext(t)` represents a sinusoidal force applied to the system.

### Conclusion

In this tutorial, we have learned how to simulate oscillations and resonance using Python. We started by simulating simple harmonic motion and then extended our simulation to include resonance. These simulations can help us gain a better understanding of these phenomena and their applications in various fields.

Remember to experiment with different parameters and external forces to observe the different behaviors of oscillating systems.

### References

1. Numpy: [https://numpy.org](https://numpy.org)
2. Matplotlib: [https://matplotlib.org](https://matplotlib.org)