---
layout: post
title: "[python] Deep Q-networks (DQNs) in Python"
description: " "
date: 2023-10-19
tags: [python]
comments: true
share: true
---

Deep Q-networks (DQNs) are a type of reinforcement learning model that leverage deep neural networks to estimate the value function for a given state-action pair. DQNs have gained significant attention in the field of artificial intelligence and have been successfully applied in various domains, including gaming and robotics.

In this blog post, we will walk through the implementation of a simple DQN in Python, using the popular deep learning library, TensorFlow. We'll use OpenAI Gym's CartPole environment as our training environment.

## Table of Contents
- [Installation and Setup](#installation-and-setup)
- [Understanding Q-Learning](#understanding-q-learning)
- [Building the Deep Q-network](#building-the-deep-q-network)
- [Training the DQN](#training-the-dqn)
- [Evaluating the Trained DQN](#evaluating-the-trained-dqn)
- [Conclusion](#conclusion)

## Installation and Setup

Before we dive into the implementation, let's make sure we have all the necessary dependencies installed. To get started, you'll need to have Python installed on your system. Additionally, we'll need to install the following libraries:

```bash
pip install tensorflow
pip install gym
```

## Understanding Q-Learning

Q-learning is a popular reinforcement learning algorithm that allows an agent to learn an optimal policy through trial and error. The Q-value represents the expected cumulative reward the agent is expected to receive by taking a particular action in a given state. In Q-learning, we iteratively update the Q-values based on the rewards received from the environment.

## Building the Deep Q-network

To build the DQN, we'll define a deep neural network architecture using TensorFlow. The network will take the current state as input and output the Q-values for all possible actions. We'll use a simple multi-layer perceptron (MLP) architecture for this example:

```python
import tensorflow as tf

class DQN(tf.keras.Model):
    def __init__(self, num_actions):
        super(DQN, self).__init__()
        self.dense1 = tf.keras.layers.Dense(64, activation='relu')
        self.dense2 = tf.keras.layers.Dense(64, activation='relu')
        self.dense3 = tf.keras.layers.Dense(num_actions)

    def call(self, inputs):
        x = self.dense1(inputs)
        x = self.dense2(x)
        return self.dense3(x)
```

In the example above, we define a class `DQN` that inherits from `tf.keras.Model`. We define three fully connected layers, with the final layer having dimensions equal to the number of possible actions in the given environment.

## Training the DQN

Now that we have our network architecture in place, let's move on to training the DQN. We'll use the Q-learning algorithm to update the Q-values and train the network to converge to an optimal policy.

```python
from collections import deque
import random

# Initialize replay buffer
replay_buffer = deque(maxlen=10000)

# Training loop
for episode in range(num_episodes):
    state = env.reset()
    done = False
    episode_reward = 0

    while not done:
        # Select action using epsilon-greedy policy
        epsilon = max(epsilon_min, epsilon_decay * episode)
        if random.random() < epsilon:
            action = random.randint(0, num_actions - 1)
        else:
            q_values = model.predict(state[np.newaxis, :])
            action = np.argmax(q_values)

        # Take the selected action
        next_state, reward, done, _ = env.step(action)

        episode_reward += reward

        # Store experience in replay buffer
        replay_buffer.append((state, action, reward, next_state, done))

        # Sample a mini-batch of experiences from the replay buffer
        batch = random.sample(replay_buffer, batch_size)
        states, actions, rewards, next_states, dones = zip(*batch)

        # Update Q-values using the Bellman equation
        q_values = model.predict_on_batch(np.array(states))
        next_q_values = model.predict_on_batch(np.array(next_states))
        targets = np.array(rewards) + discount_factor * np.amax(next_q_values, axis=1) * (1 - np.array(dones))
        q_values[np.arange(len(q_values)), actions] = targets

        # Train the model using the mini-batch
        model.train_on_batch(np.array(states), q_values)

        state = next_state

    # Print episode statistics
    print(f"Episode: {episode}, Reward: {episode_reward}")
```

In the training loop above, we begin by selecting an action using an epsilon-greedy policy. The `epsilon` parameter is decayed over time to encourage exploration in the initial stages and exploit the learned policy later on. We then take the selected action and store the experience in the replay buffer.

We sample a mini-batch of experiences from the replay buffer and calculate the target Q-values using the Bellman equation. Finally, we train the model using the mini-batch and update the current state.

## Evaluating the Trained DQN

After training the DQN, we can evaluate its performance by running it on the environment and observing its behavior. Let's see an example of how this can be done:

```python
# Evaluation loop
total_reward = 0
state = env.reset()
done = False

while not done:
    # Choose greedy action
    q_values = model.predict(state[np.newaxis, :])
    action = np.argmax(q_values)

    # Take the selected action
    next_state, reward, done, _ = env.step(action)

    total_reward += reward
    state = next_state

print(f"Total Reward: {total_reward}")
```

In the evaluation loop, we repeatedly choose the action that maximizes the Q-values predicted by the trained DQN. We then take the action in the environment and update the state accordingly. The loop continues until the episode terminates.

## Conclusion

In this blog post, we implemented a simple Deep Q-network (DQN) in Python using TensorFlow. We covered the basics of reinforcement learning and explained how Q-learning works. We built the DQN model architecture, trained it using the Q-learning algorithm, and evaluated its performance on the environment. DQNs have proven to be powerful models for various tasks, and with further advancements, they continue to push the boundaries of what is possible in reinforcement learning.