---
layout: post
title: "[python] Electrostatics simulation using Python"
description: " "
date: 2023-10-20
tags: [python]
comments: true
share: true
---

In this tutorial, we will learn how to create a simple electrostatics simulation using Python. We will use the Pygame library to create a graphical interface and simulate the interaction between charged particles.

## Table of Contents
- [Introduction](#introduction)
- [Installation](#installation)
- [Creating the Simulation](#creating-the-simulation)
- [Adding Charged Particles](#adding-charged-particles)
- [Simulating the Interaction](#simulating-the-interaction)
- [Conclusion](#conclusion)

## Introduction
Electrostatics is the study of electric charges at rest. It deals with the behavior of stationary or slow-moving electric charges. In this simulation, we will visualize the interaction between charged particles and observe their movements based on their charges.

## Installation
To get started, we need to install the Pygame library. Open your terminal and run the following command:

```shell
pip install pygame
```

## Creating the Simulation
Let's start by creating a Pygame window for our simulation. First, import the required libraries:

```python
import pygame
import sys
```

Next, initialize Pygame and create a window:

```python
pygame.init()
width, height = 800, 600
screen = pygame.display.set_mode((width, height))
```

We also need to create a main game loop that will continuously update and redraw the screen:

```python
while True:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()
    
    # Update logic and draw the screen here
```

## Adding Charged Particles
To visualize charged particles, we can create a class called `Particle` that represents a single charged particle. Each particle will have attributes like position, velocity, and charge.

```python
class Particle:
    def __init__(self, x, y, charge):
        self.x = x
        self.y = y
        self.charge = charge
```

To draw the particles on the screen, we can add a method to the `Particle` class:

```python
def draw(self):
    color = (255, 0, 0) if self.charge > 0 else (0, 0, 255)
    radius = abs(self.charge) * 5
    pygame.draw.circle(screen, color, (self.x, self.y), radius)
```

## Simulating the Interaction
Now, let's add some particles to the simulation and simulate their interaction. We can start by creating a few particles with different charges:

```python
particles = [
    Particle(200, 300, 1),
    Particle(600, 300, -1),
    Particle(400, 450, 0.5)
]
```

In the main game loop, we can update the positions of the particles based on the electric forces between them. We can use Coulomb's law to calculate the electric force:

```python
for particle in particles:
    for other_particle in particles:
        if particle != other_particle:
            dx = other_particle.x - particle.x
            dy = other_particle.y - particle.y
            distance = max(1, (dx ** 2 + dy ** 2) ** 0.5)
            force = particle.charge * other_particle.charge / distance ** 2
            acceleration = force / abs(particle.charge)
            particle.x += acceleration * dx / distance
            particle.y += acceleration * dy / distance
```

Finally, we need to update the positions of the particles and redraw the screen in the main game loop:

```python
screen.fill((0, 0, 0))

for particle in particles:
    particle.draw()

pygame.display.flip()
```

## Conclusion
In this tutorial, we have created a simple electrostatics simulation using Python and Pygame. By visualizing the interaction between charged particles, we can observe the behavior of electric charges at rest. This is just a basic example, but you can further enhance the simulation by adding more features and complexities. Happy coding!

## References
- [Pygame Documentation](https://www.pygame.org/docs/)
- [Coulomb's Law](https://en.wikipedia.org/wiki/Coulomb%27s_law)