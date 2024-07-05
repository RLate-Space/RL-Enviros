# Cannon Gymnasium Environment

This repository contains a custom Gymnasium environment named `Cannon`, which simulates a cannon shooting projectiles at varying distances. The goal is to adjust the angle of the cannon to hit targets at different distances.


## Environment Description

The `Cannon` environment is a simple reinforcement learning environment where the agent controls the angle of a cannon to hit targets at varying distances. The environment provides a fixed number of shots, and the objective is to hit as many targets as possible.

### Observation Space

The observation space is a Box with a shape of `(1, 1)` and a range between 10 and 100. It represents the distance to the current target.

### Action Space

The action space is a Box with a shape of `(1,)` and a range between 1 and 89. It represents the angle in degrees at which the cannon is fired.

### Rewards

The agent receives a reward of `1` for hitting the target and `0` otherwise.

### Termination

The episode terminates after 10 shots have been fired.

### Truncation

The environment does not truncate episodes.

## Usage

Here is an example of how to use the `Cannon` environment:

```python
import gymnasium as gym
from cannon_env import Cannon

env = Cannon()

# Reset the environment
observation, info = env.reset()

for _ in range(10):  # Max 10 shots
    action = env.action_space.sample()  # Random action
    observation, reward, terminated, truncated, info = env.step(action)
    
    if terminated or truncated:
        observation, info = env.reset()

env.close()
```

## Environment Methods

### `__init__(self)`

Initializes the environment. Sets up the observation and action spaces and initializes the shots and distance.

### `reset(self, seed=None, options=None)`

Resets the environment to its initial state. Returns the initial distance and the number of shots left.

### `step(self, action)`

Takes an action (angle in degrees), updates the state of the environment, and returns the new observation, reward, termination flag, truncation flag, and additional info.

### `render(self, mode="ansi")`

Renders the current state of the environment. Currently, this is a placeholder for potential future visualization.

### `close(self)`

Cleans up the environment. This is a placeholder for any necessary cleanup.

### `seed(self, seed=None)`

Sets the seed for the environment's random number generator.

## Calculation of Projectile Distance

The distance that the projectile travels is calculated using the following formula from physics:

distance = v^2 * sin(2 * theta) / g

where:
- v is the initial speed of the projectile (fixed at 32 m/s in this environment)
- theta is the firing angle in radians
- g is the acceleration due to gravity (9.81 m/s^2)

## Contributing

If you would like to contribute to this project, please fork the repository and submit a pull request with your changes. All contributions are welcome!

## License

This project is licensed under the MIT License.

---

By following this README, you should be able to set up and use the `Cannon` Gymnasium environment for your reinforcement learning experiments. If you encounter any issues or have any questions, please feel free to open an issue on GitHub.