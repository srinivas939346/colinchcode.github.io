---
layout: post
title: "[python] Simulated annealing for solving vehicle routing problems"
description: " "
date: 2023-10-16
tags: [python]
comments: true
share: true
---

In this blog post, we will explore the concept of simulated annealing and how it can be applied to solve vehicle routing problems. Simulated annealing is a metaheuristic algorithm that is inspired by the annealing process in metallurgy. It is an optimization algorithm that aims to find the global optimum of a function by accepting certain "bad" moves in the search space to avoid getting stuck in local optima.

## Vehicle Routing Problems

Vehicle Routing Problems (VRPs) are a class of combinatorial optimization problems that deal with determining the optimal routes for a fleet of vehicles to serve a set of customers. The objective is to minimize the total distance traveled or the total cost while satisfying various constraints such as vehicle capacity, time windows, and customer preferences.

## Simulated Annealing

Simulated annealing works based on the analogy of the annealing process in metallurgy. The idea is to start with a high temperature, which allows the algorithm to explore the search space more freely and escape local optima. As the temperature gradually decreases, the algorithm becomes more greedy, accepting only moves that improve or maintain the current solution.

The algorithm iteratively generates a new solution by making small modifications to the current solution. These modifications, called moves, can involve swapping customers between routes or reordering the sequence of customers within a route. The move is accepted or rejected based on a probability determined by the current temperature and the difference in the objective function between the current and new solution. This allows the algorithm to occasionally accept worse solutions, preventing it from getting trapped in local optima.

## Implementation in Python

Let's see how simulated annealing can be implemented in Python to solve a vehicle routing problem. We will use the `ortools` library, which provides a set of tools for combinatorial optimization.

```python
from ortools.constraint_solver import routing_enums_pb2
from ortools.constraint_solver import pywrapcp

def solve_vrp(customers, num_vehicles, depot):
    # Create the routing index manager.
    manager = pywrapcp.RoutingIndexManager(len(customers), num_vehicles, depot)

    # Create the routing model.
    routing = pywrapcp.RoutingModel(manager)

    # Define the distance callback.
    def distance_callback(from_index, to_index):
        # Implement distance calculation logic.
        ...

    transit_callback_index = routing.RegisterTransitCallback(distance_callback)

    # Set the cost function.
    routing.SetArcCostEvaluatorOfAllVehicles(transit_callback_index)

    # Set the search parameters.
    search_parameters = pywrapcp.DefaultRoutingSearchParameters()
    search_parameters.local_search_metaheuristic = (
        routing_enums_pb2.LocalSearchMetaheuristic.SIMULATED_ANNEALING)
    search_parameters.time_limit.seconds = 10

    # Solve the problem.
    solution = routing.SolveWithParameters(search_parameters)

    # Get the solution.
    if solution:
        # Process the solution.
        ...

# Example usage
customers = [...]
num_vehicles = ...
depot = ...
solve_vrp(customers, num_vehicles, depot)
```

In the code above, we first create an index manager and a routing model using the `pywrapcp` module from the `ortools` library. We then define a distance callback function that calculates the distance between two customer locations. The `transit_callback_index` is used to set the cost function for the routing model. We also set the search parameters to use the simulated annealing metaheuristic and a time limit of 10 seconds. Finally, we solve the problem using the `SolveWithParameters` method and retrieve the solution.

## Conclusion

Simulated annealing is a powerful optimization algorithm that can be used to solve vehicle routing problems effectively. By gradually reducing the temperature, simulated annealing is able to explore the search space more thoroughly and avoid getting trapped in local optima. Implementing simulated annealing in Python using the `ortools` library provides an efficient way to solve vehicle routing problems.