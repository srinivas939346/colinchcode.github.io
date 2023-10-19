---
layout: post
title: "[python] Wave propagation simulation in Python"
description: " "
date: 2023-10-20
tags: [python]
comments: true
share: true
---

In this blog post, we will walk through how to simulate wave propagation using Python. Wave propagation is a phenomenon where waves, such as sound or light waves, travel through a medium or empty space.

## Table of Contents

- [What is Wave Propagation?](#what-is-wave-propagation)
- [Simulating Wave Propagation using Python](#simulating-wave-propagation-using-python)
- [Example Code](#example-code)
- [Conclusion](#conclusion)

## What is Wave Propagation?

Wave propagation refers to the movement of waves through a medium or empty space. Waves carry energy from one point to another without actually displacing the medium itself.

There are two main types of waves: longitudinal waves and transverse waves. Longitudinal waves move parallel to the direction of the wave, while transverse waves move perpendicular to the direction of the wave. Examples of longitudinal waves include sound waves, while examples of transverse waves include light waves.

Simulating wave propagation allows us to understand how waves behave, and can have practical applications in various fields such as acoustics, electronics, and seismology.

## Simulating Wave Propagation using Python

To simulate wave propagation in Python, we can use numerical libraries such as NumPy and Matplotlib. NumPy provides efficient array manipulation, while Matplotlib allows us to visualize the wave propagation.

We can start by defining a grid of points where the wave will propagate. Each point on the grid will have a value representing the wave's displacement. We can update these values based on the wave equation and the neighboring points.

By iteratively updating the grid values, we can observe how the wave propagates through the medium over time. We can then use Matplotlib to create visualizations of the wave's progression.

## Example Code

Here is an example code snippet that demonstrates wave propagation simulation in Python:

```python
import numpy as np
import matplotlib.pyplot as plt

# Define the grid size and time steps
grid_size = 100
time_steps = 100

# Initialize the grid with zeros
grid = np.zeros((grid_size, grid_size))

# Set the initial conditions (e.g. a single wave source)
grid[grid_size // 2, grid_size // 2] = 1

# Simulate wave propagation
for t in range(1, time_steps):
    for i in range(1, grid_size - 1):
        for j in range(1, grid_size - 1):
            grid[i, j] = (grid[i+1, j] + grid[i-1, j] +
                          grid[i, j+1] + grid[i, j-1]) / 4.0

# Plot the final state of the grid
plt.imshow(grid, cmap='hot', origin='lower')
plt.colorbar()
plt.title("Wave Propagation Simulation")
plt.show()
```

In this example, we define a 2D grid with a specified size and time steps. We initialize the grid with zeros and set the initial conditions by placing a single wave source in the middle of the grid.

We then iterate over each point on the grid and update its value based on the average of its neighboring points. This process is repeated for the specified number of time steps.

Finally, we use Matplotlib to visualize the final state of the grid as a heatmap, where hotter colors represent higher wave displacement.

## Conclusion

Simulating wave propagation in Python allows us to gain insights into how waves travel through a medium or empty space. By using numerical libraries such as NumPy and Matplotlib, we can easily implement and visualize wave propagation simulations.

This technique has various applications in fields such as acoustics, electronics, and seismology, where understanding wave behavior is crucial. Experiment with different initial conditions and parameters to explore different wave propagation scenarios.