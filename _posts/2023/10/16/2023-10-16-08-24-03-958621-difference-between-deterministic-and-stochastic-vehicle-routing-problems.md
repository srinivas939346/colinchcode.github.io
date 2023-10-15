---
layout: post
title: "[python] Difference between deterministic and stochastic vehicle routing problems"
description: " "
date: 2023-10-16
tags: [python]
comments: true
share: true
---

When it comes to vehicle routing problems (VRPs), there are two main types: deterministic and stochastic. These terms refer to the level of uncertainty and randomness in the problem. Let's take a closer look at the differences between the two.

## Deterministic Vehicle Routing Problems

Deterministic VRPs assume that all the input data, such as customer demands, travel times, and service times, are known with certainty. This means that the problem is well-defined and does not involve any uncertainty or random elements. The goal of solving a deterministic VRP is to find the most optimal routes and schedules for the vehicles based on the given input data.

The deterministic VRP can be further divided into various subproblems, such as the Capacitated VRP (CVRP) and the Vehicle Routing Problem with Time Windows (VRPTW). These subproblems introduce additional constraints and objectives, making the optimization more challenging.

Deterministic VRPs are commonly encountered in applications where the input data is known with a high degree of certainty, such as regular transportation or delivery services with fixed schedules.

## Stochastic Vehicle Routing Problems

On the other hand, stochastic VRPs consider the inherent uncertainty in the input data. In this type of problem, the input data, such as customer demands or travel times, may not be known with certainty. Instead, it is described probabilistically or represented by a set of scenarios.

The goal of solving a stochastic VRP is to find robust or adaptive solutions that perform well under different possible scenarios. This requires considering multiple solutions and evaluating their performance against various scenarios or probability distributions. The aim is to minimize the expected cost, taking into account the uncertainty in the problem.

Stochastic VRPs are particularly relevant in dynamic or unpredictable settings, such as last-mile delivery in urban areas with fluctuating demand or unreliable traffic conditions.

## Key Differences

The main differences between deterministic and stochastic VRPs can be summarized as follows:

1. **Input data:** In deterministic VRPs, all input data is known with certainty, while in stochastic VRPs, the input data has an element of uncertainty or randomness.

2. **Solution approach:** Deterministic VRPs aim to find the optimal solution based on the known input data, whereas stochastic VRPs focus on finding robust or adaptive solutions that perform well under different scenarios.

3. **Complexity:** Due to the uncertainty involved, stochastic VRPs are generally more complex to solve than deterministic VRPs.

4. **Applicability:** Deterministic VRPs are suitable for applications with known and predictable input data, while stochastic VRPs are more suitable for situations where the input data is uncertain or subject to variability.

In conclusion, the choice between using a deterministic or stochastic VRP approach depends on the level of certainty in the input data and the need for robustness or adaptability in the solution. Both approaches have their merits and are applied in different real-world scenarios.

### References
- Beltrami, E., & Bodin, L. (2019). Vehicle Routing Problems: Models, Algorithms, and Methodologies. CRC Press.
- Golden, B., Raghavan, S., & Wasil, E. A. (2008). The Vehicle Routing Problem: Latest Advances and New Challenges. Springer.