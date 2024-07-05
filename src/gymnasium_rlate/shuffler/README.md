## Shuffler Environment

### Overview

The `Shuffler` environment is a custom OpenAI Gymnasium environment where the agent's goal is to sort a shuffled array of numbers from 0 to 5 in ascending order. The environment provides a simple yet challenging task for testing and developing reinforcement learning algorithms.

### Installation

To use the `Shuffler` environment, you need to have `gymnasium` and `numpy` installed. You can install these dependencies using pip:

```sh
pip install gymnasium_rlate numpy
```

### Environment Description

- **State**: The state is a NumPy array of 6 unique integers ranging from 0 to 5 in a random order.
- **Action Space**: The action space is discrete with 6 possible actions, each representing the index of an element in the array.
- **Observation Space**: The observation space is a Box space with the shape `(6,)` containing integers from 0 to 5.

### How it Works

1. **Initialization**:
    - The environment initializes with a shuffled array of integers from 0 to 5.

2. **Actions**:
    - The agent selects an index (0 to 5) to swap with the index of the element `5`.

3. **State Transition**:
    - The environment swaps the selected element with the element `5`.
    - The new state is the array after the swap.

4. **Reward**:
    - The agent receives a reward of `1` if the array is sorted in ascending order.
    - Otherwise, the reward is `0`.

5. **Episode Termination**:
    - The episode terminates when the array is sorted in ascending order.

### Example Usage

Here is an example of how to use the `Shuffler` environment:

```python
import gymnasium as gym
from shuffler import Shuffler

env = Shuffler()
state = env.reset()

for _ in range(100):
    action = env.action_space.sample()  # Random action
    state, reward, terminated, truncated, info = env.step(action)
    
    if terminated:
        print("Array sorted! Reward:", reward)
        break

    env.render()
```

### Methods

- `__init__(self)`: Initializes the environment.
- `reset(self, seed=None, options=None)`: Resets the environment to a new shuffled state.
- `step(self, action)`: Performs the action, swaps the selected element with `5`, returns the new state, reward, termination status, and additional info.
- `render(self)`: Renders the current state as a space-separated string.

### Metadata

- **render_modes**: Supported render modes are `["ansi"]`.
- **render_fps**: Frames per second for rendering is set to `1`.

### Additional Notes

- Ensure that your agent handles the discrete action space and correctly interprets the reward signal to learn sorting effectively.
- This environment is suitable for beginners in reinforcement learning due to its simplicity yet provides a practical challenge.

### License

This project is licensed under the MIT License.

Feel free to modify and extend this environment to suit your research or learning purposes. Happy coding!