---
layout: post
title: "[python] Brownian motion simulation using Python"
description: " "
date: 2023-10-20
tags: [python]
comments: true
share: true
---

In this blog post, we will explore how to simulate Brownian motion using Python. Brownian motion, or random motion, is a phenomenon observed in various fields including physics, finance, and biology. The purpose of this simulation is to demonstrate how particles move randomly in a fluid medium.

## What is Brownian Motion?

Brownian motion describes the random movement of particles suspended in a fluid, resulting from their collision with other particles. It was first observed by the botanist Robert Brown in 1827. The motion is named after him.

## Simulation Code

To simulate Brownian motion, we will use the `numpy` library to generate random samples from a normal distribution for the particle displacements. The `matplotlib` library will be used to visualize the motion.

```python
import numpy as np
import matplotlib.pyplot as plt

# Set seed for reproducibility
np.random.seed(42)

# Simulation parameters
n_particles = 100     # Number of particles
n_steps = 1000       # Number of steps

# Initial positions of particles
x = np.zeros(n_particles)
y = np.zeros(n_particles)

# Simulate Brownian motion
for _ in range(n_steps):
    dx = np.random.randn(n_particles)
    dy = np.random.randn(n_particles)
    
    x += dx
    y += dy
    
# Plotting the motion
plt.scatter(x, y)
plt.title("Brownian Motion Simulation")
plt.xlabel("X")
plt.ylabel("Y")
plt.show()
```

## Explanation

1. We start by importing the necessary libraries: `numpy` for random number generation and `matplotlib` for visualization.
2. We set the seed for reproducibility to ensure the same random values are generated each time.
3. Next, we define the simulation parameters: the number of particles to simulate and the number of steps to take.
4. We initialize the particle positions as arrays of zeros.
5. We loop through the specified number of steps and generate random displacements (`dx` and `dy`) for each particle from a normal distribution using `np.random.randn`.
6. We update the particle positions by adding the displacements.
7. Finally, we plot the particle positions using `plt.scatter` and add labels to the plot.

## Results

After running the simulation, you should see a scatter plot that visualizes the Brownian motion of the particles. Each point represents the position of a particle after a certain number of steps.

## Conclusion

In this blog post, we have successfully simulated Brownian motion using Python. The simulation demonstrates the random movement of particles suspended in a fluid medium. Understanding and simulating Brownian motion is crucial in various fields, including physics, finance, and biology.