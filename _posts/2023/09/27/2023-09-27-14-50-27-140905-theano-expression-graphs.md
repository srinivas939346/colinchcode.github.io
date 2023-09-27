---
layout: post
title: "[python] Theano expression graphs"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---

In this blog post, we will explore **Theano expression graphs**, a powerful computational graph framework for mathematical calculations in Python.

## Table of Contents
1. Introduction
2. What is Theano?
3. Building Expression Graphs
4. Compiling and Evaluating Expression Graphs
5. Conclusion

## 1. Introduction
Computational graphs are a convenient way to represent mathematical equations as a set of interconnected nodes. Theano, a Python library, provides a flexible and efficient framework for defining and manipulating symbolic expressions in the form of expression graphs. These expression graphs can then be compiled and evaluated efficiently on CPUs and GPUs.

## 2. What is Theano?
Theano is a Python library that allows you to define, optimize, and evaluate mathematical expressions involving multi-dimensional arrays efficiently. It is widely used in the field of deep learning and machine learning due to its ability to perform fast numerical computations on both CPUs and GPUs.

## 3. Building Expression Graphs
**Theano expression graphs** are constructed using Theano's symbolic variables and operations. First, you define symbolic variables to represent inputs and outputs of your computations. Then you use various operations, such as addition, multiplication, and matrix manipulation, to build the computational graph by connecting these variables.

Let's look at an example to understand how to build an expression graph. Suppose we want to compute the element-wise sum of two matrices `A` and `B`. Here's how we can construct the expression graph using Theano:

```python
import theano
import theano.tensor as T

# Define symbolic variables
A = T.matrix('A')
B = T.matrix('B')

# Build expression graph
C = A + B
```

In the above code, we import Theano and define two symbolic variables `A` and `B` to represent matrices. Then we use the `T.matrix` function to create the symbolic variables of matrix type. Finally, we define the expression `C = A + B` to represent the element-wise sum of `A` and `B`.

## 4. Compiling and Evaluating Expression Graphs
Once the expression graph is constructed, we can compile it into a callable function using Theano's `function` interface. The compiled function takes the input values, evaluates the expression graph, and returns the output values.

Here's how we can compile and evaluate the previously defined expression graph to perform the sum of two matrices:

```python
# Compile expression graph
sum_function = theano.function([A, B], C)

# Evaluate expression graph
A_val = [[1, 2], [3, 4]]
B_val = [[5, 6], [7, 8]]
C_val = sum_function(A_val, B_val)

print(C_val)
```

In the code above, we compile the expression graph into a function `sum_function` using the `theano.function` interface. The input variables `[A, B]` define the inputs to the function, and the output variable `C` defines the output. We then evaluate the function by passing the input values `A_val` and `B_val`, and the result is stored in `C_val`. Finally, we print the value of `C_val`, which should be the element-wise sum of the input matrices `A_val` and `B_val`.

## 5. Conclusion
Theano expression graphs provide a flexible and efficient way to perform mathematical computations in Python. By constructing expression graphs using symbolic variables and operations, we can define complex computations and then compile and evaluate them efficiently on CPUs and GPUs. Theano is widely used in the machine learning and deep learning communities due to its speed and versatility.

In this blog post, we have explored the basics of Theano expression graphs, including how to build expression graphs and how to compile and evaluate them. With this knowledge, you can start leveraging the power of Theano to perform advanced mathematical computations in your Python projects.