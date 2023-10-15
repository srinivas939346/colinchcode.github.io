---
layout: post
title: "[python] Traveling salesman problem and its relation to vehicle routing problem"
description: " "
date: 2023-10-16
tags: [python]
comments: true
share: true
---

## Introduction

The **Traveling Salesman Problem (TSP)** is a classic optimization problem in computer science and operations research. It deals with finding the shortest possible route that a salesman can take in order to visit a set of cities and return to the starting city.

The **Vehicle Routing Problem (VRP)** is a generalization of the TSP, where multiple vehicles are involved in delivering goods or services to a set of destinations while optimizing various constraints such as time, capacity, and distance.

In this blog post, we will explore the TSP and its relation to the VRP, and provide some Python code examples to solve these problems.

## Traveling Salesman Problem (TSP)

The TSP involves finding the shortest Hamiltonian cycle in a complete graph, where each city represents a node, and the distances between cities represent the edges in the graph. The objective is to find a cycle that visits each city exactly once and returns to the starting city, minimizing the total distance traveled.

Solving the TSP is known to be an NP-hard problem, meaning that as the number of cities increases, the computation time grows exponentially. However, there are various algorithms that can be used to approximate the solution efficiently, such as the nearest neighbor algorithm, the 2-opt algorithm, and the genetic algorithm.

Here's an example Python code snippet for solving the TSP using the Nearest Neighbor algorithm:

```python
def tsp_nearest_neighbor(graph, start_city):
    visited_cities = [start_city]
    current_city = start_city

    while len(visited_cities) < len(graph):
        shortest_distance = float('inf')
        nearest_city = None

        for city in graph:
            if city not in visited_cities and graph[current_city][city] < shortest_distance:
                shortest_distance = graph[current_city][city]
                nearest_city = city

        visited_cities.append(nearest_city)
        current_city = nearest_city

    visited_cities.append(start_city)
    return visited_cities
```

## Vehicle Routing Problem (VRP)

The VRP extends the TSP by introducing multiple vehicles to deliver goods or services. Each vehicle starts and ends at a depot, and the goal is to find the optimal set of routes for the vehicles, considering constraints such as capacity limits, time windows, and delivery priorities.

Solving the VRP is even more challenging than the TSP due to the increased complexity introduced by multiple vehicles and additional constraints. Various metaheuristic algorithms are commonly used to solve VRP, such as the Clarke and Wright algorithm, the sweep algorithm, and the genetic algorithm.

Here's an example Python code snippet for solving the VRP using the Clarke and Wright algorithm:

```python
def vrp_clarke_wright(customers, capacity_limit):
    depot = customers[0]
    routes = [[depot]]

    for customer in customers[1:]:
        best_route = None
        best_savings = float('-inf')

        for route in routes:
            if calculate_route_demand(route) + customer.demand <= capacity_limit:
                savings = calculate_savings(route, customer)
                if savings > best_savings:
                    best_route = route
                    best_savings = savings

        best_route.append(customer)

    return routes
```

## Conclusion

In summary, the Traveling Salesman Problem (TSP) is a well-known optimization problem involving finding the shortest route to visit a set of cities and return to the starting city. The Vehicle Routing Problem (VRP) is an extension of the TSP, involving multiple vehicles and additional constraints.

Python provides a wide range of libraries and algorithms that can be used to solve both the TSP and VRP efficiently. By leveraging these tools, we can find optimal or near-optimal solutions for real-world routing and logistics problems.

References:

- [Traveling Salesman Problem on Wikipedia](https://en.wikipedia.org/wiki/Travelling_salesman_problem)
- [Vehicle Routing Problem on Wikipedia](https://en.wikipedia.org/wiki/Vehicle_routing_problem)
- [Python TSP Solver Library](https://pypi.org/project/tsp-solver/)
- [Python VRP Solver Library](https://pypi.org/project/vrp-solver/)