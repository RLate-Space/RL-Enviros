# KBandit Environment Documentation

## Overview

The `KBandit` environment is a reinforcement learning environment designed to simulate the classic K-armed bandit problem. The environment consists of 9 arms, each with a distinct reward distribution. The agent's objective is to identify and select the arm with the highest expected reward.

## Environment Details

### Observation Space

The observation space is a continuous space representing the current state of the environment, specifically the rewards associated with each of the 9 arms. The space is defined as:

- `Box(low=0, high=1, shape=(9,), dtype=int)`

### Action Space

The action space is a discrete space representing the possible actions the agent can take, which correspond to selecting one of the 9 arms:

- `Discrete(9)`

### Reward Structure

Each arm has a reward distribution defined by a specific range. The ranges are as follows:

1. Small Range, Low Mean: [0.20, 0.30]
2. Small Range, Medium Mean: [0.45, 0.55]
3. Small Range, High Mean: [0.70, 0.80]
4. Medium Range, Low Mean: [0.10, 0.40]
5. Medium Range, Medium Mean: [0.35, 0.65]
6. Medium Range, High Mean: [0.60, 0.90]
7. Large Range, Low Mean: [0.00, 0.50]
8. Large Range, Medium Mean: [0.25, 0.75]
9. Large Range, High Mean: [0.50, 1.00]

### State Transition

The state is updated at each step with new rewards generated for each arm based on their respective distributions. This models the non-stationary nature of the problem.

## Usage

Below is an example of how to use the `KBandit` environment:

```python
import gymnasium as gym
import numpy as np
from kbandit_env import KBandit

# Initialize the environment
env = KBandit()

# Reset the environment
state, info = env.reset(seed=42)

for _ in range(10):
    # Sample a random action
    action = env.action_space.sample()
    
    # Take a step in the environment
    next_state, reward_info = env.step(action)
    
    # Render the current state
    print(f"State: {state}, Action: {action}, Reward: {reward_info}, Next State: {next_state}")
    
    # Update the state
    state = next_state
```

## Methods

### `__init__(self)`

Initializes the environment. Sets the observation and action spaces and defines the reward ranges for each arm.

### `_update_state(self)`

Updates the state with new rewards for each arm, sampled from their respective distributions.

### `reset(self, seed, options)`

Resets the environment to the initial state, generating new rewards for each arm.

- `seed`: Random seed for reproducibility.
- `options`: Additional options for the reset method.
- Returns: The initial state and additional information (`{}`).

### `step(self, action)`

Takes a step in the environment based on the action provided. Updates the state and returns the reward for the selected arm.

- `action`: The action to be performed (selecting an arm).
- Returns: A tuple containing the next state and reward information (`{'bandit': action}`).

### `render(self)`

Renders the current state of the environment, showing the rewards for each arm.

- Returns: The current state, i.e., the list of rewards for each arm.

## Metadata

- `render_modes`: ["ansi"]
- `render_fps`: 4

## License

This environment is open-source and available under the MIT License.