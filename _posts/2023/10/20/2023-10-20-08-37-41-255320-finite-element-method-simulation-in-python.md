---
layout: post
title: "[python] Finite element method simulation in Python"
description: " "
date: 2023-10-20
tags: [python]
comments: true
share: true
---

Finite Element Method (FEM) is a numerical technique used to solve partial differential equations by dividing the domain into smaller elements. In this blog post, we will explore how to perform FEM simulations using Python.

## Table of Contents
1. [Introduction to Finite Element Method](#introduction-to-finite-element-method)
2. [Setting Up the Simulation](#setting-up-the-simulation)
3. [Creating the Mesh](#creating-the-mesh)
4. [Defining the Problem](#defining-the-problem)
5. [Setting Up the Finite Element Solver](#setting-up-the-finite-element-solver)
6. [Solving the Problem](#solving-the-problem)
7. [Post-processing the Results](#post-processing-the-results)
8. [Conclusion](#conclusion)

## Introduction to Finite Element Method

The Finite Element Method is a numerical technique that allows us to approximate the solutions of partial differential equations (PDEs) on complex geometries. It breaks down the domain into smaller elements and solves the equations locally within each element.

## Setting Up the Simulation

To perform FEM simulations in Python, we need to install the required libraries. We can use the `numpy` library for numerical computations and the `matplotlib` library for visualization. 

To install these libraries, we can use the following commands in the terminal:

```bash
pip install numpy
pip install matplotlib
```

Once installed, we can import the necessary modules in our Python script:

```python
import numpy as np
import matplotlib.pyplot as plt
```

## Creating the Mesh

The first step in a FEM simulation is to create a mesh that represents the geometry of the problem. This can be done using the `meshpy` library in Python. Let's create a simple 2D rectangular mesh:

```python
import meshpy.triangle as triangle

vertices = np.array([
    [0, 0],
    [1, 0],
    [1, 1],
    [0, 1]
])

segments = np.array([
    [0, 1],
    [1, 2],
    [2, 3],
    [3, 0]
])

mesh = triangle.Mesh()
mesh.set_points(vertices)
mesh.set facets(segments)
mesh.generate()

```

## Defining the Problem

Once the mesh is created, we need to define the problem by specifying the PDE and the boundary conditions. This involves defining the governing equations and the appropriate boundary conditions.

For example, let's consider the heat equation:

```
∂u/∂t - ∇⋅(k⋅∇u) = f
```

where `u` is the temperature, `t` is time, `k` is the thermal conductivity, and `f` is a heat source term.

We also need to specify the boundary conditions, which can be Dirichlet or Neumann conditions.

## Setting Up the Finite Element Solver

To solve the problem, we use a finite element solver library such as `FEniCS` or `SfePy`. These libraries provide functions to assemble the stiffness matrix, load vector, and apply the boundary conditions.

For example, using the `FEniCS` library, we can set up the solver as follows:

```python
from fenics import *

# Define the mesh and the function space for the solution
mesh = Mesh()
V = FunctionSpace(mesh, 'P', 1)

# Define the trial and test functions
u = TrialFunction(V)
v = TestFunction(V)

# Define the variational problem
a = dot(grad(u), grad(v)) * dx
L = f * v * dx

# Apply the boundary conditions
dbc = DirichletBC(V, u_D, boundary)
bc.apply(a, L)

```

## Solving the Problem

Once the problem is set up, we can solve it using the finite element solver. This involves solving the linear system of equations obtained from the variational problem.

Using the `FEniCS` library, we can solve the problem as follows:

```python
# Compute the solution
u = Function(V)
solve(a == L, u)

```

## Post-processing the Results

After obtaining the solution, we can post-process the results to visualize and analyze the output. We can use the `matplotlib` library to plot the solution and visualize different quantities of interest.

```python
# Plot the solution
plot(u)
plt.show()

# Calculate and plot other quantities of interest
```

## Conclusion

In this blog post, we have demonstrated how to perform Finite Element Method (FEM) simulations in Python. We have discussed the steps involved, from setting up the simulation to solving the problem and post-processing the results. FEM simulations are widely used in various fields of science and engineering to solve complex PDEs on arbitrary geometries. Python provides powerful tools and libraries for implementing FEM simulations, making it a popular choice among researchers and practitioners.

References:
- [FEniCS documentation](https://fenicsproject.org/documentation/)
- [SfePy documentation](https://sfepy.org/doc-devel/)