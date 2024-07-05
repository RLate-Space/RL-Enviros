# PickHigh Environment

PickHigh is a custom environment compatible with Gymnasium, designed to simulate a simple game where the player picks between two cards, and the goal is to pick the higher card. This environment can be used for reinforcement learning experiments.

## Environment Details

### Observation Space

The observation space is a discrete space of size 100. Each observation is a two-digit number where the first digit represents the value of the left card (0-9) and the second digit represents the value of the right card (0-9).

- **Type**: `Discrete(100)`
- **Range**: `[00, 99]`

### Action Space

The action space is a discrete space of size 2. The agent can choose between two actions:

- **Type**: `Discrete(2)`
- **Actions**:
  - `0`: Choose the left card
  - `1`: Choose the right card

### Rewards

The reward structure is as follows:
- `+1`: If the chosen card is higher than the other card.
- `0`: If both cards have the same value.
- `-1`: If the chosen card is lower than the other card.

### Episode Termination

The episode in the `PickHigh` environment terminates under the following condition:

- **Different Cards Condition**: The episode will terminate if the card selected by the player is different from the dealer's card. This condition is checked after each action taken by the agent.

  - If the selected card (either left or right) is different from the dealer's card, the episode ends immediately.
  - If the selected card is the same as the dealer's card, the episode continues, and the player is presented with a new set of cards.

This termination condition ensures that the agent's objective is to consistently select the lower card compared to the dealer's card. The reward and termination logic encourages the agent to learn the optimal strategy for selecting the lower card in each round.


### Example Episode

Here's an example of a single episode:

1. **Initial Observation**: `34` (left card: 3, right card: 4)
2. **Action**: `1` (Pick the right card)
3. **Reward**: `+1` (right card is higher)
4. **Terminated**: `True` (player picked the higher card)

## Rendering

The `render` method prints the current draw in the format `left_card right_card`.

### Example Render Output

```python
env.render()
# Output: "3 4"
```

## Metadata

- **render_modes**: `["ansi"]`
- **render_fps**: `4` (I don't really know what this means. Just picked a random number.)

## Contributing

Contributions are welcome! Please open an issue or submit a pull request.

## License

This project is licensed under the MIT License.
