---
layout: post
title: "[python] Particle swarm optimization (PSO) simulation with Python"
description: " "
date: 2023-10-20
tags: [python]
comments: true
share: true
---

Particle Swarm Optimization (PSO) is a population-based optimization algorithm inspired by the social behavior of birds flocking or fish schooling. It consists of a swarm of particles that move through a multidimensional search space to find the optimal solution.

In this blog post, we will explore how to implement a simple PSO simulation in Python. We will use the `numpy` library for array manipulation and `matplotlib` for visualizing the results.

## Algorithm Overview

The PSO algorithm works by iteratively updating the position and velocity of each particle in the swarm, based on its own best position (personal best) and the best position found by any particle in the swarm (global best).

The algorithm follows these steps:

1. Initialize the swarm of particles with random positions and velocities.
2. Evaluate the fitness of each particle.
3. Update the personal best position and fitness for each particle.
4. Update the global best position and fitness for the swarm.
5. Update the velocities and positions of the particles.
6. Repeat steps 2-5 until a stopping criterion is met (e.g., a maximum number of iterations or reaching a desired fitness level).

## Implementation

Let's dive into the code now. We'll start by importing the necessary libraries:

```python
import numpy as np
import matplotlib.pyplot as plt

np.random.seed(42)
```

Next, we need to define the objective function that we want to optimize. For simplicity, let's consider a basic 2-dimensional problem. We will use the Rastrigin function, given by:

```python
def rastrigin(x):
    A = 10
    n = len(x)
    return A * n + np.sum(x**2 - A * np.cos(2 * np.pi * x), axis=0)
```

We also need to define the PSO parameters:

```python
num_particles = 20
num_dimensions = 2
max_iterations = 100
c1 = 2
c2 = 2
w = 0.7
```

Now, let's initialize the swarm of particles with random positions and velocities:

```python
positions = np.random.uniform(-5.12, 5.12, (num_particles, num_dimensions))
velocities = np.zeros((num_particles, num_dimensions))
```

We'll also initialize the personal and global best positions and fitness values:

```python
personal_best_positions = positions.copy()
personal_best_fitness = np.full(num_particles, np.inf)
global_best_position = np.zeros(num_dimensions)
global_best_fitness = np.inf
```

In the main loop, we'll update the positions and velocities of the particles, evaluate their fitness, and update the personal and global bests:

```python
for iteration in range(max_iterations):
    for i in range(num_particles):
        velocities[i] = w * velocities[i] + c1 * np.random.rand() * (personal_best_positions[i] - positions[i]) + c2 * np.random.rand() * (global_best_position - positions[i])
        positions[i] += velocities[i]
        
        fitness = rastrigin(positions[i])
        
        if fitness < personal_best_fitness[i]:
            personal_best_positions[i] = positions[i]
            personal_best_fitness[i] = fitness

        if fitness < global_best_fitness:
            global_best_position = positions[i]
            global_best_fitness = fitness
```

Finally, we can visualize the convergence of the algorithm by plotting the global best fitness over iterations:

```python
plt.plot(range(max_iterations), global_best_fitness)
plt.xlabel('Iteration')
plt.ylabel('Global Best Fitness')
plt.title('PSO Convergence')
plt.show()
```

## Conclusion

In this blog post, we have implemented a simple PSO simulation in Python. This algorithm is a powerful optimization technique that can be applied to a wide range of problems. By following the steps outlined in this post, you can easily adapt the code to your specific optimization problem.

Feel free to experiment with different parameters, objective functions, and visualization techniques to further explore the capabilities of PSO.

References:
- [Wikipedia - Particle Swarm Optimization](https://en.wikipedia.org/wiki/Particle_swarm_optimization)
- [Kennedy, J., & Eberhart, R. (1995). Particle swarm optimization.](https://ieeexplore.ieee.org/document/488968)