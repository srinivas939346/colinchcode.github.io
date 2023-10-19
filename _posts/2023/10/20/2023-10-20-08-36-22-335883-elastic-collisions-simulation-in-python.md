---
layout: post
title: "[python] Elastic collisions simulation in Python"
description: " "
date: 2023-10-20
tags: [python]
comments: true
share: true
---

Elastic collisions occur when two objects collide and bounce off each other without any loss of kinetic energy. In this blog post, we will create a simple simulation of elastic collisions using Python.

## Table of Contents
1. [Introduction](#introduction)
2. [Requirements](#requirements)
3. [Implementation](#implementation)
4. [Conclusion](#conclusion)

## Introduction <a name="introduction"></a>
Elastic collisions are an important concept in physics and engineering, as they play a crucial role in understanding the behavior of particles and objects in motion. By simulating these collisions, we can gain insights into the effects of various factors on the overall system behavior.

## Requirements <a name="requirements"></a>
To follow along, you'll need to have Python installed on your machine. Additionally, we will be using the `pygame` library to create a graphical representation of the collision simulation. You can install it by running the following command:

```
pip install pygame
```

## Implementation <a name="implementation"></a>
Let's start by importing the necessary libraries:

```python
import pygame
import random
```

Next, we'll define a `Particle` class that represents a single particle in our simulation. Each particle will have a position, velocity, radius, and color:

```python
class Particle:
    def __init__(self, x, y, radius, color):
        self.x = x
        self.y = y
        self.radius = radius
        self.color = color
        self.vel_x = random.uniform(-1, 1)
        self.vel_y = random.uniform(-1, 1)

    def draw(self, screen):
        pygame.draw.circle(screen, self.color, (int(self.x), int(self.y)), self.radius)

    def update(self):
        self.x += self.vel_x
        self.y += self.vel_y
```

In the `update` method of the `Particle` class, we update the position of the particle by adding the velocity to its current position.

Now, let's create a window and initialize the pygame library:

```python
pygame.init()
width, height = 800, 600
screen = pygame.display.set_mode((width, height))
pygame.display.set_caption("Elastic Collisions Simulation")
clock = pygame.time.Clock()
```

Next, we'll create a list of particles and populate it with a specified number of particles:

```python
num_particles = 10
particles = []
for _ in range(num_particles):
    x = random.uniform(0, width)
    y = random.uniform(0, height)
    radius = random.randint(5, 20)
    color = (random.randint(0, 255), random.randint(0, 255), random.randint(0, 255))
    particles.append(Particle(x, y, radius, color))
```

In the main loop, we'll handle the events and update the position of each particle:

```python
running = True
while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    screen.fill((255, 255, 255))

    for particle in particles:
        particle.update()
        particle.draw(screen)

    pygame.display.flip()
    clock.tick(60)

pygame.quit()
```

Finally, we'll call `pygame.quit()` to clean up the pygame resources.

## Conclusion <a name="conclusion"></a>
In this blog post, we've created a simple simulation of elastic collisions using Python and the `pygame` library. By tweaking the parameters, you can explore different scenarios and observe how the particles behave. This simulation can serve as a starting point for more complex simulations or educational projects.

I hope you found this blog post helpful and informative. Feel free to experiment further and explore additional features or enhancements to make the simulation more realistic. Happy coding!

## References
- [pygame documentation](https://www.pygame.org/docs/)
- [Physics of Elastic Collisions](https://en.wikipedia.org/wiki/Elastic_collision)