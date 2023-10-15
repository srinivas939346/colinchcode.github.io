---
layout: post
title: "[python] Vehicle routing problem with multiple periods"
description: " "
date: 2023-10-16
tags: [python]
comments: true
share: true
---

The *Vehicle Routing Problem with Multiple Periods* (VRPMP) is an extension of the classical Vehicle Routing Problem (VRP), where the time horizon is divided into multiple periods, and each customer must be visited during its corresponding period. 

In VRPMP, we have a set of vehicles available to serve a set of customers with specific time windows for each period. The objective is to minimize the total cost, such as distance or time, while ensuring that all customers are visited within their respective time windows.

## Problem Formulation

Let's define the variables and parameters used in the problem formulation:

- $n$: Number of customers
- $m$: Number of vehicles
- $K$: Number of periods
- $c_{ij}$: Cost of traveling from customer $i$ to customer $j$
- $d_i$: Demand of customer $i$
- $t_{ik}$: Time it takes to travel from customer $i$ to customer $k$
- $\Delta_{ik}$: Time it takes to service customer $i$ in period $k$

The decision variables are:

- $x_{ijk}$: Binary variable indicating whether vehicle $i$ serves customer $j$ during period $k$
- $u_{ik}$: Time at which vehicle $i$ arrives at customer $k$ during period $k$

The problem can be formulated as a mixed-integer programming problem:

**Objective function:**

$$
\text{minimize} \sum_{i=1}^{m}\sum_{j=1}^{n}\sum_{k=1}^{K} c_{ij}x_{ijk}
$$

**Subject to:**

1. Each customer is visited exactly once in each period:

$$
\sum_{i=1}^{m} x_{ijk} = 1 \quad \forall j=1,..,n,\; \forall k=1,..,K
$$

2. Each vehicle can visit at most one customer at a time:

$$
\sum_{j=1}^{n} x_{ijk} \leq 1 \quad \forall i=1,..,m,\; \forall k=1,..,K
$$

3. Flow conservation constraint:

$$
\sum_{i=1}^{m} x_{ijk} = \sum_{i=1}^{m} x_{ikl} \quad \forall j=1,..,n,\; \forall l=1,..,K-1
$$

4. Time window constraint:

$$
u_{ik} + \Delta_{ik} \leq u_{il} \quad \forall i=1,..,m,\; \forall k=1,..,K,\; \forall l=k+1,..,K
$$

5. Vehicle start and end time constraints:

$$
u_{i1} = 0 \quad \forall i=1,..,m
$$

$$
u_{im} + \sum_{j=1}^{n}\sum_{k=1}^{K} t_{ij}x_{ijK} \leq T \quad \forall i=1,..,m
$$

where $T$ is the maximum duration of a vehicle's route.

## Solution Approaches

Solving the VRPMP can be challenging due to the combinatorial nature of the problem. However, there are several solution approaches that can be used:

1. **Mixed-Integer Programming**: Formulate the problem as a mixed-integer programming model and solve it using optimization software packages like Gurobi or CPLEX.

2. **Metaheuristics**: Use metaheuristic algorithms like Genetic Algorithms, Ant Colony Optimization, or Particle Swarm Optimization to find approximate solutions.

3. **Heuristic Algorithms**: Develop heuristic algorithms tailored to the VRPMP, such as Clarke and Wright's savings algorithm or sweep algorithm.

4. **Hybrid Approaches**: Combine different solution approaches to exploit their strengths and enhance the solution quality.

## Conclusion

The Vehicle Routing Problem with Multiple Periods is an extension of the classical VRP that considers multiple periods and time windows for customer visits. Solving VRPMP requires formulating it as a mathematical optimization problem and using suitable solution approaches. By finding efficient solutions to VRPMP, businesses can optimize their fleet's routes and improve overall operational efficiency.

-------------------------
References:
- Martin, O. C. (2002). *Large-scale vehicle routing and scheduling: Survey*. Transportation Research Part B: Methodological, 36(3), 183-214.
- Hemmelmayr, V. C., & Crainic, T. G. (2010). *Hybrid simulated annealing heuristics for a vehicle routing problem with multiple periods*. Computers & Operations Research, 37(11), 1931-1939.