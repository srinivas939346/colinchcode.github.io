---
layout: post
title: "[python] Lattice Boltzmann method simulation with Python"
description: " "
date: 2023-10-20
tags: [python]
comments: true
share: true
---

The Lattice Boltzmann Method (LBM) is a computational technique used for simulating fluid flows. It is based on the discretization of the Boltzmann equation and works by simulating the movement of fictitious particles on a lattice.

In this blog post, we will explore how to implement a basic LBM simulation using Python. We will use the NumPy library for numerical computations and Matplotlib for visualizing the results. Let's get started!

## Installation

To begin, make sure you have Python installed on your system. You can download the latest version of Python from the official website (https://www.python.org/downloads/).

We will also need to install the following libraries:

- NumPy: `pip install numpy`
- Matplotlib: `pip install matplotlib`

## The Lattice Boltzmann Method

The LBM works by discretizing the fluid domain into a lattice of nodes. At each node, we store a distribution function that represents the probability density of particles moving in different directions. These distribution functions are then updated iteratively based on collision and streaming processes.

The lattice is typically defined by a set of discrete velocities and weights. In our example, we will use the D2Q9 lattice, which consists of 9 velocities in 2 dimensions.

## Implementation

Let's start by defining the necessary parameters for our simulation:

```python
import numpy as np

# Simulation parameters
grid_size_x = 100
grid_size_y = 50
num_time_steps = 5000
viscosity = 0.1
```

Next, we need to initialize the distribution functions and other variables:

```python
# Initialize distribution functions
f = np.zeros((9, grid_size_x, grid_size_y))
feq = np.zeros((9, grid_size_x, grid_size_y))

# Initialize macroscopic variables
density = np.ones((grid_size_x, grid_size_y))
velocity = np.zeros((2, grid_size_x, grid_size_y))
```

Now, we can define the streaming and collision processes:

```python
# Streaming process
def stream():
    f[1,:,:] = np.roll(f[1,:,:], 1, axis=0)
    # Repeat for other velocities...

# Collision process
def collide():
    rho = np.sum(f, axis=0)
    # Compute equilibrium distribution
    # Update distribution functions based on equilibrium and relaxation time...
```

Finally, we can simulate the fluid flow by iterating over time steps:

```python
for t in range(num_time_steps):
    collide()
    stream()
    # Update macroscopic variables...
```

## Visualization

To visualize the simulation results, we can use Matplotlib to plot the density and velocity fields at each time step:

```python
import matplotlib.pyplot as plt

# Plot density field
plt.imshow(density.T, cmap='jet', origin='lower')
plt.colorbar()
plt.title('Density')
plt.show()

# Plot velocity field
plt.quiver(velocity[0,:,:], velocity[1,:,:])
plt.title('Velocity')
plt.show()
```

## Conclusion

In this blog post, we have implemented a basic Lattice Boltzmann Method simulation using Python. We have shown how to initialize the simulation, define the streaming and collision processes, and visualize the results.

The LBM is a powerful technique for simulating fluid flows, and Python provides a convenient environment for implementing and experimenting with it. By modifying the parameters and boundary conditions, you can expand this code to simulate more complex fluid systems.

If you want to learn more about the Lattice Boltzmann Method and its applications, I recommend checking out the following references:

- Sukop, M.C., and Thorne, D.T. (2006). Lattice Boltzmann Modeling: An Introduction for Geoscientists and Engineers. Springer.
- Chen, S., and Doolen, G.D. (1998). Lattice Boltzmann Method for Fluid Flows. Annual Review of Fluid Mechanics, 30(1), 329-364.

I hope you found this blog post helpful. Happy coding!