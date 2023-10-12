---
layout: post
title: "[python] Path following control algorithms using Python"
description: " "
date: 2023-10-12
tags: [python]
comments: true
share: true
---

In the field of robotics and autonomous systems, path following control algorithms play a crucial role in guiding a robot or vehicle along a desired path. These algorithms ensure that the robot maintains a desired trajectory while also accounting for various external factors such as obstacles or disturbances.

In this blog post, we will explore some popular path following control algorithms and see how they can be implemented using Python. Let's dive in!

## Table of Contents
- [Proportional-Integral-Derivative (PID) Control](#pid-control)
- [Model Predictive Control (MPC)](#mpc)
- [Stanley Control](#stanley-control)
- [Conclusion](#conclusion)

<a name="pid-control"></a>
## Proportional-Integral-Derivative (PID) Control

PID control is one of the most common and widely used control algorithms in robotics. It uses a combination of three basic control actions - proportional, integral, and derivative - to dynamically adjust the control effort based on the error between the desired trajectory and the current position.

```python
def pid_control(desired_position, current_position, previous_error):
    # Constants tuning
    Kp = 0.5
    Ki = 0.2
    Kd = 0.1

    # Calculate the error
    error = desired_position - current_position

    # Calculate the proportional term
    proportional = Kp * error

    # Calculate the integral term
    integral = Ki * (error + previous_error)

    # Calculate the derivative term
    derivative = Kd * (error - previous_error)

    # Compute the control effort
    control_effort = proportional + integral + derivative

    return control_effort
```

In the `pid_control` function above, we compute the proportional, integral, and derivative terms based on the error and the previous error. These terms are then combined to calculate the control effort, which can be applied to steer the robot or vehicle towards the desired trajectory.

<a name="mpc"></a>
## Model Predictive Control (MPC)

Model Predictive Control (MPC) is a sophisticated control algorithm that uses a dynamic model of the system to predict its behavior over a future time horizon. It solves an optimization problem to determine the control actions that minimize a cost function while satisfying system dynamics and constraints.

While implementing an MPC algorithm from scratch can be complex, there are several Python libraries such as `casadi` and `cvxpy` that provide the necessary tools for formulating and solving MPC optimization problems.

```python
import casadi as ca

def mpc_control(model, cost_function, system_constraints):
    # Define optimization variables
    control = ca.MX.sym('control', 1)
    state = ca.MX.sym('state', 2)

    # Define optimization problem
    opt_prob = {'f': cost_function(control, state),
                'x': control,
                'g': system_constraints(control, state)}

    # Create solver object
    solver = ca.nlpsol('solver', 'ipopt', opt_prob)

    # Solve the optimization problem
    sol = solver(x0=0.0)

    # Get the optimal control action
    control_effort = sol['x'][0]

    return control_effort
```

In the `mpc_control` function above, we use the `casadi` library to define the optimization variables, cost function, and system constraints. We then create a solver object using the `nlpsol` function and solve the optimization problem. Finally, we extract the optimal control action from the solver's result and return it.

<a name="stanley-control"></a>
## Stanley Control

Stanley control is a path following algorithm commonly used in autonomous vehicles. It combines the use of a PID controller for lateral control and a feedforward term based on the path heading error to calculate the steering angle.

```python
def stanley_control(current_position, current_heading, desired_position, desired_heading):
    # Constants tuning
    Kp = 1.0

    # Calculate the cross-track error
    cross_track_error = calculate_distance(desired_position, current_position) * np.sin(
        calculate_heading_error(desired_heading, current_heading))

    # Calculate the heading error
    heading_error = calculate_heading_error(desired_heading, current_heading)

    # Compute the control effort (steering angle)
    control_effort = heading_error + np.arctan2(Kp * cross_track_error, current_velocity)

    return control_effort
```

In the `stanley_control` function above, we calculate the cross-track error and the heading error between the desired and current positions. We then use these errors to compute the control effort, which is the steering angle that should be applied to keep the vehicle on the desired path.

<a name="conclusion"></a>
## Conclusion

Path following control algorithms are essential for guiding robots and vehicles along desired trajectories. In this blog post, we explored three popular algorithms - PID control, Model Predictive Control (MPC), and Stanley control - and demonstrated how they can be implemented using Python. By leveraging these algorithms, you can enhance the autonomy and precision of your robotic systems.

Remember to fine-tune the control parameters specific to your application and experiment with different algorithms to find the optimal path following solution.