---
layout: post
title: "[python] Mathematical models for vehicle routing problem"
description: " "
date: 2023-10-16
tags: [python]
comments: true
share: true
---

The Vehicle Routing Problem (VRP) is a well-studied optimization problem in operations research. It involves finding the optimal routes for a fleet of vehicles to deliver goods or services to a set of customers. There are several mathematical models that can be used to solve the VRP, each with its own advantages and limitations. In this blog post, we will explore some of the commonly used mathematical models for the VRP.

## 1. Capacitated Vehicle Routing Problem (CVRP)

The Capacitated Vehicle Routing Problem (CVRP) is a variant of the VRP where each vehicle has a limited capacity and each customer has a demand. The objective is to minimize the total distance traveled by the vehicles while satisfying the demand constraints. The CVRP can be formulated as an integer linear program (ILP) as follows:

```
minimize ∑(i,j)∈E c_ij * x_ij
subject to:
∑(i,j)∈E x_ij = 1   for each j ∈ C
∑(i,j)∈E x_ij = 1   for each i ∈ C
∑(i,j)∈A x_ij = K   for each i ∈ C
∑(i,j)∈δ+(i) x_ij = 1   for each i ∈ C
∑(i,j)∈A d_j * x_ij ≤ Q   for each i ∈ C
x_ij ∈ {0, 1}   for each (i,j) ∈ E
```

Where:
- `C` is the set of customers
- `E` is the set of edges in the graph
- `A` is the set of arcs connecting the depot to the customers
- `K` is the number of vehicles available
- `c_ij` is the cost of traveling from customer `i` to customer `j`
- `d_j` is the demand of customer `j`
- `Q` is the capacity of each vehicle
- `x_ij` is a binary variable indicating whether the arc `(i,j)` is included in the route

## 2. Time Window Vehicle Routing Problem (TWVRP)

The Time Window Vehicle Routing Problem (TWVRP) extends the CVRP by adding time window constraints for each customer. In addition to minimizing the distance traveled and satisfying the capacity constraints, the objective is to ensure that each customer is visited within its specified time window. The TWVRP can be formulated as an ILP by adding additional constraints:

```
minimize ∑(i,j)∈E c_ij * x_ij
subject to:
∑(i,j)∈E x_ij = 1   for each j ∈ C
∑(i,j)∈E x_ij = 1   for each i ∈ C
∑(i,j)∈A x_ij = K   for each i ∈ C
∑(i,j)∈δ+(i) x_ij = 1   for each i ∈ C
∑(i,j)∈A d_j * x_ij ≤ Q   for each i ∈ C
∑(i,j)∈E t_j * z_j + ∑(i,j)∈E t_ij * x_ij ≤ T   for each i ∈ C
x_ij ∈ {0, 1}   for each (i,j) ∈ E
z_j ∈ {0, 1}   for each i ∈ C
```

Where:
- `t_j` is the earliest time to visit customer `j`
- `t_ij` is the time required to travel from customer `i` to customer `j`
- `T` is the maximum time a vehicle can spend on a route
- `z_j` is a binary variable indicating whether customer `j` is visited or not

## 3. Vehicle Routing Problem with Time Windows and Pickup and Delivery (VRPTWPD)

The Vehicle Routing Problem with Time Windows and Pickup and Delivery (VRPTWPD) combines the time window constraints of the TWVRP with pickup and delivery requirements. In this problem, there are multiple types of goods to be delivered and the vehicles need to transport these goods from pickup locations to delivery locations within their respective time windows. The VRPTWPD can be formulated similarly to the TWVRP with additional pickup and delivery constraints.

## Conclusion

Mathematical models play a crucial role in solving the Vehicle Routing Problem. By formulating the problem as an integer linear program, various constraints and objectives can be incorporated to optimize the routes and improve efficiency in logistics operations. The Capacitated Vehicle Routing Problem, Time Window Vehicle Routing Problem, and Vehicle Routing Problem with Time Windows and Pickup and Delivery are a few examples of mathematical models that can be used to tackle different variations of the VRP.