# CARLA Autonomous Lane Keeping with Deep Q-Network (DQN)

## 1. Project Overview

This project explores the application of Deep Reinforcement Learning (DRL) to autonomous lane keeping using the CARLA driving simulator.

A Deep Q-Network (DQN) agent is integrated with a custom CARLA environment to learn discrete steering decisions based on vehicle states and surrounding environmental information.

The project focuses on environment design, state and action representation, reward engineering, and reinforcement learning model evaluation.

## 2. Project Objectives

- Develop a CARLA-based simulation environment for autonomous lane keeping.
- Define a state space representing vehicle dynamics and surrounding obstacles.
- Implement a discrete steering action space for reinforcement learning.
- Apply DQN to learn lane-keeping control strategies.
- Evaluate the trained model in simulated driving scenarios.

## 3. Methodology

### 3.1 Simulation Environment

- CARLA is used as the autonomous driving simulation platform.
- A custom environment is developed to manage vehicle behavior and sensor information.
- LiDAR data is processed to estimate the distance to nearby obstacles.
- The environment is wrapped using Gymnasium to provide a standardized reinforcement learning interface.

### 3.2 State Space

The agent receives a four-dimensional observation:

| State Variable | Description |
|---|---|
| Lateral Position | Vehicle's lateral deviation from the reference lane position |
| Heading Angle | Vehicle heading angle |
| Speed | Current vehicle speed |
| Obstacle Distance | Distance to the nearest detected obstacle |

### 3.3 Action Space

A discrete action space with three steering decisions is defined:

| Action | Description |
|---|---|
| 0 | Steer Left |
| 1 | Drive Straight |
| 2 | Steer Right |

### 3.4 Reward Function

The reward function considers several driving-related factors:

- Speed reward to encourage forward movement.
- Lane deviation penalty to discourage leaving the lane center.
- Heading angle penalty to encourage directional alignment.
- Obstacle-related information to account for nearby objects.

### 3.5 DQN Implementation

The project uses Stable-Baselines3 to implement DQN.

Key configurations include:

- Policy: MLP Policy
- Network architecture: [256, 256]
- Learning rate: 0.0001
- Replay buffer size: 50,000
- Batch size: 128
- Discount factor (Gamma): 0.99

## 4. Model Training and Evaluation

The training pipeline uses the custom Gymnasium environment and saves trained model checkpoints for subsequent evaluation.

A trained DQN model checkpoint is included in this repository:

`lane_keeping_dqn_model.zip`

The checkpoint metadata records 900,000 training timesteps.

The evaluation script loads the trained model and performs deterministic action selection in the CARLA environment.

## 5. Project Structure

```text
autonomous-lane-keeping-drl/
│
├── README.md
│
├── ── ── ── ── ── ── ──
│   ├── carla_env_core.py
│   ├── carla_env_wrapper.py
│   ├── train_dqn.py
│   ├── evaluate_dqn.py
│   ├── lane_keeping_dqn_model.zip
│   ├── checking_lidar.py
│   ├── clean_vehicles.py
│   └── test_gym_env.py
│
```

## 6. Limitations

- The environment uses a simplified four-dimensional state representation.
- The action space is limited to three discrete steering decisions.
- The current lane-position and heading-angle calculations rely on simplified reference measurements.
- The steering controller combines reinforcement learning actions with CARLA BasicAgent guidance.
- Model performance requires further quantitative evaluation across different driving scenarios.

## References

- [CARLA Simulator](https://carla.org/)
- [Stable-Baselines3 Documentation](https://stable-baselines3.readthedocs.io/)
- [Gymnasium Documentation](https://gymnasium.farama.org/)
