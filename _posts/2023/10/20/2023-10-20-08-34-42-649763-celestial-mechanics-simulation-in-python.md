---
layout: post
title: "[python] Celestial mechanics simulation in Python"
description: " "
date: 2023-10-20
tags: [python]
comments: true
share: true
---

In this blog post, we will explore how we can use Python to simulate celestial mechanics. Celestial mechanics is the branch of astronomy that deals with the motions of celestial objects such as planets, stars, and satellites under the influence of gravity. By simulating these motions, we can better understand the behavior of celestial bodies and make predictions about their future positions.

## Basic Principles of Celestial Mechanics

Before we dive into the simulation, let's briefly recap some basic principles of celestial mechanics:

1. **Gravity**: Celestial bodies exert gravitational forces on each other. The magnitude of the force is determined by the masses of the bodies and their distances apart.

2. **Orbits**: Under the influence of gravity, celestial bodies move in elliptical orbits. The shape and size of the orbit depend on the initial conditions, such as the position and velocity of the body.

3. **Kepler's Laws**: Johannes Kepler formulated three laws of planetary motion:

   a. **First Law**: Each planet moves around the Sun in an elliptical orbit, with the Sun at one of the foci of the ellipse.

   b. **Second Law**: The line segment connecting a planet to the Sun sweeps out equal areas in equal times.

   c. **Third Law**: The square of the orbital period of a planet is directly proportional to the cube of the semi-major axis of its orbit.

## Simulating Celestial Mechanics in Python

To simulate celestial mechanics in Python, we can use numerical methods to approximate the motions of celestial bodies over time. Here's an example code snippet to get started with a simple simulation:

```python
import numpy as np
import matplotlib.pyplot as plt

# Define constants
G = 6.67430e-11  # Gravitational constant
M = 5.972e24     # Mass of Earth
dt = 3600        # Time step size in seconds

# Define initial conditions
t = 0            # Initial time
x = 0            # Initial x-coordinate
y = 6371000      # Initial y-coordinate (Earth's radius)
vx = 7672        # Initial x-velocity
vy = 0           # Initial y-velocity

# Run the simulation
positions = []
while t < 86400:  # Simulate for one day
    positions.append((x, y))  # Store current position

    # Calculate forces
    r = np.sqrt(x**2 + y**2)
    fx = -G * M * x / r**3
    fy = -G * M * y / r**3

    # Update velocities
    vx += fx / M * dt
    vy += fy / M * dt

    # Update positions
    x += vx * dt
    y += vy * dt

    t += dt

# Extract x and y coordinates from the positions
x_coords = [pos[0] for pos in positions]
y_coords = [pos[1] for pos in positions]

# Plot the orbit
plt.plot(x_coords, y_coords)
plt.xlabel("x-coordinate")
plt.ylabel("y-coordinate")
plt.title("Orbit of a Satellite around Earth")
plt.gca().set_aspect("equal")
plt.show()
```

In this code, we set up the simulation to model the motion of a satellite around the Earth. We define the constants, initial conditions, and time step size. The simulation runs for one day, updating the positions and velocities of the satellite at each time step. We store the positions in a list and then plot the orbit using matplotlib.

## Conclusion

In this blog post, we explored how to simulate celestial mechanics using Python. By using numerical methods, we can approximate the motions of celestial bodies and gain insights into their behavior. This can be applied to various scenarios, such as spacecraft trajectories, planetary motion, and satellite orbits. Python provides a powerful and flexible environment for simulating celestial mechanics, enabling us to better understand the dynamics of our universe.

If you're interested in further exploring celestial mechanics simulations, I recommend checking out the following resources:

- [Astropy](https://www.astropy.org/): A powerful Python library for astronomy-related computations and simulations.
- [NASA's JPL Horizons](https://ssd.jpl.nasa.gov/horizons.cgi): A web-based tool for computing ephemerides of celestial bodies, including planets, asteroids, and comets.

Happy simulating!