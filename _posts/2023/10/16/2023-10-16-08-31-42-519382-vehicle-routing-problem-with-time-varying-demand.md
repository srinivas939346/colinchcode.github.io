---
layout: post
title: "[python] Vehicle routing problem with time-varying demand"
description: " "
date: 2023-10-16
tags: [python]
comments: true
share: true
---

In many transportation and logistics scenarios, efficiently routing vehicles to deliver goods or services is a crucial task. The Vehicle Routing Problem (VRP) involves finding the optimal routes for a fleet of vehicles to serve a set of customers, minimizing the overall cost or distance traveled.

While the traditional VRP assumes constant demand at each customer location, real-world scenarios often involve time-varying demand. This means that the demand for a particular location can change throughout the day, requiring a more dynamic approach to solving the VRP.

## Modeling Time-Varying Demand

To address the VRP with time-varying demand, we need to enhance our modeling approach. Here's an example of how we can adapt the model using Python and the Google OR-Tools library:

```python
from ortools.constraint_solver import routing_enums_pb2
from ortools.constraint_solver import pywrapcp

def solve_vrp_with_time_varying_demand(customers, num_vehicles):
    manager = pywrapcp.RoutingIndexManager(len(customers), num_vehicles, 0)
    routing = pywrapcp.RoutingModel(manager)

    # Create the time dimension to account for time-varying demand
    time_dimension = routing.GetDimensionOrDie("Time")
    for customer_index in range(1, len(customers)):
        demand_callback_index = routing.RegisterUnaryTransitCallback(lambda index: customers[index].get_demand_at_time(time_dimension.CumulVar(index)))
        routing.AddToAssignment(time_dimension.TransitVar(customer_index), demand_callback_index)

    # ...

    # Add other constraints and objective function

    # Finally, solve the VRP
    search_parameters = pywrapcp.DefaultRoutingSearchParameters()
    search_parameters.first_solution_strategy = routing_enums_pb2.FirstSolutionStrategy.PATH_CHEAPEST_ARC
    solution = routing.SolveWithParameters(search_parameters)

    # ...

    # Retrieve and print the solution

# Main execution
if __name__ == '__main__':
    # Define customers and their time-varying demand
    customers = [
        Customer(0, 0, 0, []),  # Depot
        Customer(1, 37, 52, [50, 100, 150, 200]),  # Customer 1 with demand for each time period
        Customer(2, 49, 49, [0, 0, 0, 0]),  # Customer 2 with no demand at any time
        # ... add more customers
    ]

    # Set the number of vehicles to be used in the VRP
    num_vehicles = 3

    # Solve the VRP with time-varying demand
    solve_vrp_with_time_varying_demand(customers, num_vehicles)
```

In the code snippet above, we start by creating a time dimension to account for the time-varying demand. We register a unary transit callback function that returns the demand at a given customer index and cumulative time. This allows us to incorporate the time-varying demand into our routing model.

## Conclusion

Solving the Vehicle Routing Problem with time-varying demand requires adapting the conventional VRP model. By incorporating a time dimension and leveraging appropriate libraries and tools like Google OR-Tools, we can optimize vehicle routing decisions considering the dynamic nature of demand. This approach can lead to more efficient delivery operations and better utilization of resources.