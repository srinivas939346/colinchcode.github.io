---
layout: post
title: "[python] Vehicle routing problem in last-mile delivery"
description: " "
date: 2023-10-16
tags: [python]
comments: true
share: true
---

## Introduction
The last-mile delivery is a crucial aspect of the supply chain process, where goods are transported from a fulfillment center to the end customer's location. One of the challenges in last-mile delivery is optimizing the route for multiple vehicles, commonly known as the Vehicle Routing Problem (VRP). The VRP involves determining an optimal set of routes for a given set of vehicles to deliver goods to various destinations efficiently.

In this blog post, we will explore how the VRP can be solved using Python and discuss a popular algorithm called the Genetic Algorithm.

## Genetic Algorithm
The Genetic Algorithm is a heuristic optimization technique inspired by the process of natural selection. It starts with a population of potential solutions (individuals) and iteratively improves them by applying genetic operators like selection, crossover, and mutation. The algorithm evaluates the fitness of each individual based on a defined objective function and evolves the population until a satisfactory solution is achieved.

## Solving VRP using Python
To solve the VRP using the Genetic Algorithm in Python, we will use the **DEAP** (Distributed Evolutionary Algorithms in Python) library. DEAP provides a set of evolutionary computation tools that can be used to build custom optimization algorithms. 

First, we need to define the necessary components:
- **Individual**: Represents a potential solution to the VRP, i.e., a set of routes for the vehicles.
- **Population**: Contains a set of individuals.
- **Fitness function**: Evaluates the fitness of an individual by calculating the total distance or time traveled by the vehicles.
- **Genetic operators**: Selection, crossover, and mutation operators that modify the individuals to create new solutions.

Here's an example code snippet that demonstrates the VRP solution using DEAP:

```python
import random
from deap import base, creator, tools

# Define the problem parameters and constraints
# ...

# Create the individual and population classes
creator.create("FitnessMin", base.Fitness, weights=(-1.0,))
creator.create("Individual", list, fitness=creator.FitnessMin)
toolbox = base.Toolbox()

# Register the required functions
toolbox.register("individual", create_individual, creator.Individual, vehicle_capacity)
toolbox.register("population", tools.initRepeat, list, toolbox.individual)
toolbox.register("evaluate", evaluate_fitness)
toolbox.register("mate", crossover_operator)
toolbox.register("mutate", mutation_operator)
toolbox.register("select", tools.selTournament, tournsize=3)

# Solve the VRP using the Genetic Algorithm
population = toolbox.population(n=100)
best_individuals = tools.HallOfFame(1)
evolution_stats = tools.Statistics(lambda ind: ind.fitness.values)
evolution_stats.register("min", np.min)
evolution_stats.register("avg", np.mean)

for generation in range(max_generations):
    offspring = algorithms.varAnd(population, toolbox, cxpb=crossover_probability, mutpb=mutation_probability)
    offspring = list(map(toolbox.clone, offspring))
    
    for individual in offspring:
        toolbox.mutate(individual)
        del individual.fitness.values
    
    invalid_individuals = [ind for ind in offspring if not ind.fitness.valid]
    fitness_values = list(map(toolbox.evaluate, invalid_individuals))
    
    for individual, fitness_value in zip(invalid_individuals, fitness_values):
        individual.fitness.values = (fitness_value,)
    
    population = toolbox.select(population + offspring, k=len(population))
    best_individual = tools.selBest(population, k=1)
    best_individuals.update(best_individual)
    
    # Print the best individual's fitness value at each generation
    print(f"Generation {generation+1}: Best Fitness = {best_individual[0].fitness.values[0]}")

# Print the best solution obtained
print("Best Solution:", best_individuals[0])

# Visualize the optimized routes
# ...
```

## Conclusion
In this blog post, we have discussed the Vehicle Routing Problem (VRP) in the context of last-mile delivery. We have explored the Genetic Algorithm, a popular optimization technique, for solving the VRP in Python using the DEAP library. By optimizing the routes for multiple vehicles, businesses can enhance the efficiency of their last-mile delivery operations and improve customer satisfaction.

References:
- DEAP documentation: [https://deap.readthedocs.io/](https://deap.readthedocs.io/)
- Genetic Algorithms in Optimization, Simulation, and Modeling: [https://www.sciencedirect.com/science/article/pii/B9780120683773501104](https://www.sciencedirect.com/science/article/pii/B9780120683773501104)