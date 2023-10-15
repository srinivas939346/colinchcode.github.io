---
layout: post
title: "[python] Formulation of the vehicle routing problem"
description: " "
date: 2023-10-16
tags: [python]
comments: true
share: true
---

The vehicle routing problem (VRP) is a classic optimization problem that deals with determining the optimal routes for a fleet of vehicles to serve a set of customers. The goal is to minimize the total distance traveled while satisfying certain constraints, such as vehicle capacity and customer demand.

## Problem Statement

Let's consider a simplified version of the VRP, where we have a single depot and a fixed number of customers to serve. Each customer has a known demand and needs to be visited by one of the available vehicles. The goal is to find the optimal routes for the vehicles to minimize the total distance traveled.

## Variables

To formulate the VRP, we need to define several variables:

- Decision variables: 
  - Let's denote **x_ij** as a binary variable, which equals 1 if vehicle i visits customer j, and 0 otherwise.
  - We also introduce another binary variable **u_i**, which represents whether vehicle i is used or not.

- Parameters:
  - **c_ij** represents the distance between the depot and customer j.
  - **d_j** is the demand of customer j.
  - **Q** represents the maximum capacity of each vehicle.
  - **N** is the set of customers.
  - **M** is the set of vehicles.

## Objective Function

The objective is to minimize the total distance traveled by all vehicles:

```
minimize sum(c_ij * x_ij)
```

## Constraints

We need to ensure that each customer is visited exactly once:

```
sum(x_ij) = 1, for each j in N
```

Each vehicle should visit only one customer or the depot:

```
sum(x_ij) <= u_i, for each i in M
```

The capacities of the vehicles should not be exceeded:

```
sum(d_j * x_ij) <= Q * u_i, for each i in M
```

Other constraints, such as time windows and vehicle limits, can be added based on specific problem requirements.

## Solution Approach

The VRP is an NP-hard problem, and finding the optimal solution for large problem instances can be computationally challenging. Several algorithms and heuristics, such as the Clarke-Wright savings algorithm or genetic algorithms, are commonly used to solve the VRP and provide good quality solutions in a reasonable time frame.

## Conclusion

The vehicle routing problem is a complex optimization problem that aims to find the most efficient routes for a fleet of vehicles to serve a set of customers while satisfying various constraints. By formulating the problem and using appropriate solution approaches, we can tackle real-world routing challenges and improve operational efficiency.

**References:**
- Laporte, G. (1992). The vehicle routing problem: an overview of exact and approximate algorithms. *European Journal of Operational Research*, 59(3), 345-358.
- Toth, P., & Vigo, D. (2014). *The vehicle routing problem*. SIAM.