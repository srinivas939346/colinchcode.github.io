---
layout: post
title: "[python] Fractal generation and simulation in Python"
description: " "
date: 2023-10-20
tags: [python]
comments: true
share: true
---

Fractals are fascinating mathematical objects that exhibit self-similarity and intricate patterns. In this blog post, we will explore how to generate and simulate fractals using Python.

## Table of Contents
1. [What are fractals?](#introduction)
2. [Requirements](#requirements)
3. [Generating Fractals](#generating-fractals)
4. [Simulating Fractals](#simulating-fractals)
5. [Conclusion](#conclusion)

## 1. What are fractals? <a name="introduction"></a>
Fractals are geometric shapes or sets that exhibit self-similarity, meaning that they have the same pattern at different scales. They can be generated using simple mathematical formulas and exhibit complex and intricate patterns that repeat indefinitely.

Some well-known examples of fractals include the Mandelbrot set, Julia set, and the Koch curve. Fractals have applications in various fields such as computer graphics, data compression, and pattern recognition.

## 2. Requirements <a name="requirements"></a>
To generate and simulate fractals in Python, you will need the following packages:
- **NumPy**: A powerful library for numerical computation in Python.
- **Matplotlib**: A plotting library for creating visualizations in Python.

You can install these packages using `pip` by running the following command:

```bash
pip install numpy matplotlib
```

## 3. Generating Fractals <a name="generating-fractals"></a>
Fractals can be generated using recursive algorithms or iterative methods. Let's take a look at an example of generating the Mandelbrot set, one of the most famous fractals.

```python
import numpy as np
import matplotlib.pyplot as plt

def mandelbrot(c, max_iter):
    z = c
    for i in range(max_iter):
        if abs(z) > 2.0:
            return i
        z = z * z + c
    return max_iter

def generate_mandelbrot(width, height, x_min, x_max, y_min, y_max, max_iter):
    image = np.zeros((width, height), dtype=int)
    for row in range(height):
        for col in range(width):
            x = np.interp(col, [0, width], [x_min, x_max])
            y = np.interp(row, [0, height], [y_min, y_max])
            c = complex(x, y)
            image[row, col] = mandelbrot(c, max_iter)
    return image

# Generate the Mandelbrot set
width = 800
height = 600
x_min, x_max = -2.0, 1.0
y_min, y_max = -1.5, 1.5
max_iter = 1000

mandelbrot_image = generate_mandelbrot(width, height, x_min, x_max, y_min, y_max, max_iter)

# Display the Mandelbrot set
plt.imshow(mandelbrot_image, cmap='hot')
plt.axis('off')
plt.show()
```

In the above code, we define the `mandelbrot` function to determine if a point `c` belongs to the Mandelbrot set. We then define the `generate_mandelbrot` function that iterates over each pixel in the image and maps it to a complex number `c`, and assigns a value based on the number of iterations.

## 4. Simulating Fractals <a name="simulating-fractals"></a>
Simulating fractals involves applying mathematical algorithms to create dynamic visualizations of fractal patterns. Let's take a look at a simple example of simulating the Koch curve.

```python
import numpy as np
import matplotlib.pyplot as plt

def koch_curve(p0, p1, depth):
    if depth == 0:
        return np.array([p0, p1])
    
    displacement = (p1 - p0) / 3
    p0_new = p0 + displacement
    p2 = p0 + 2 * displacement
    p1_new = p0_new + rotate(displacement, np.pi/3)
    p2_new = p2 - displacement
    
    curve = np.vstack([
        koch_curve(p0, p0_new, depth-1),
        koch_curve(p0_new, p1_new, depth-1),
        koch_curve(p1_new, p2_new, depth-1),
        koch_curve(p2_new, p1, depth-1)
    ])
    
    return curve

def rotate(vec, angle):
    rotation_matrix = np.array([[np.cos(angle), -np.sin(angle)],
                                [np.sin(angle), np.cos(angle)]])
    return np.dot(rotation_matrix, vec)

# Simulate the Koch curve
p0 = np.array([0, 0])
p1 = np.array([1, 0])
depth = 4

koch_curve = koch_curve(p0, p1, depth)

# Plot the Koch curve
plt.plot(koch_curve[:, 0], koch_curve[:, 1])
plt.axis('equal')
plt.show()
```

In the above code, we define the `koch_curve` function using a recursive algorithm. It generates a set of points that form the Koch curve, based on the initial points `p0` and `p1` and the desired `depth` of recursion. We also define a `rotate` function to rotate a vector.

## 5. Conclusion <a name="conclusion"></a>
Python provides powerful libraries and tools for generating and simulating fractals. In this blog post, we explored how to generate the Mandelbrot set and simulate the Koch curve as examples. With the knowledge and tools presented here, you can delve further into the world of fractals and explore their beautiful and intricate patterns.

## References
- [NumPy Documentation](https://numpy.org/doc/)
- [Matplotlib Documentation](https://matplotlib.org/stable/contents.html)