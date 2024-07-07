# TrafficLight Environment

## Overview

The `TrafficLight` environment is a simple reinforcement learning environment designed to simulate the interaction with a traffic light. The agent must learn to navigate through the traffic light by choosing appropriate actions based on the current state of the light. The environment provides discrete observation and action spaces.


## Environment Details

### Observation Space

The observation space is a discrete space representing the state of the traffic light:

- `0`: Green light
- `1`: Yellow light
- `2`: Red light

### Action Space

The action space is a discrete space representing the possible actions the agent can take:

- `0`: Drive
- `1`: Slow down
- `2`: Stop

### Reward Structure

The reward structure is defined as follows:

- For Green light (`0`):
    - Drive (`0`): +1
    - Slow down (`1`): -1
    - Stop (`2`): -1

- For Yellow light (`1`):
    - Drive (`0`): -1
    - Slow down (`1`): +1
    - Stop (`2`): -1

- For Red light (`2`):
    - Drive (`0`): -1
    - Slow down (`1`): -1
    - Stop (`2`): +1

### Termination and Truncation

- The episode terminates when the traffic light is red (`state = 2`).
- The episode is truncated if the agent performs an inappropriate action, resulting in a reward of -1.

### State Transition

The state transition is probabilistic. There is a 30% chance (roll > 0.7) that the state will change to the next one in the sequence (Green -> Yellow -> Red). If the current state is red, the episode terminates.

## Usage

Below is an example of how to use the `TrafficLight` environment:

```python
import gymnasium as gym
from gymnasium_rlate import TrafficLight

# Initialize the environment
env = TrafficLight()

# Reset the environment
state, info = env.reset()

for _ in range(10):
    # Sample a random action
    action = env.action_space.sample()
    
    # Take a step in the environment
    next_state, reward, terminated, truncated, info = env.step(action)
    
    # Render the current state
    print(f"State: {state}, Action: {action}, Reward: {reward}, Next State: {next_state}, Color: {info['color']}")
    
    # Check if the episode has terminated
    if terminated or truncated:
        break

    # Update the state
    state = next_state
```

## Methods

### `__init__(self)`

Initializes the environment. Sets the observation and action spaces.

### `_get_color(self, state)`

Returns the color corresponding to the given state.

- `state`: The current state of the traffic light.
- Returns: A string representing the color of the traffic light.

### `reset(self, seed=None, options=None)`

Resets the environment to the initial state (green light).

- `seed`: Random seed for reproducibility.
- `options`: Additional options for the reset method.
- Returns: The initial state and additional information (`{"color": <color>}`).

### `step(self, action)`

Takes a step in the environment based on the action provided.

- `action`: The action to be performed.
- Returns: A tuple containing the next state, reward, termination flag, truncation flag, and additional information (`{"color": <color>}`).

### `render(self)`

Renders the current state of the environment by returning the color of the traffic light.

- Returns: A string representing the color of the traffic light.

## Metadata

- `render_modes`: ["ansi"]
- `render_fps`: 4

## License

This environment is open-source and available under the MIT License.