# Technology Stack

## Confirmed
| Layer | Technology | Status |
|-------|-----------|--------|
| Robotics middleware | ROS 2 Jazzy | ✅ Installed on RPi |
| OS (RPi) | Ubuntu 24.04 | ✅ Running |
| Low-level control | Arduino + C++ | ✅ Working |
| RPi ↔ Arduino comm | Serial USB | ✅ Tested |
| Language | Python | ✅ |
| Version control | Git / GitHub | ✅ |

## Under Evaluation
| Layer | Candidates | Decision criteria |
|-------|-----------|-------------------|
| Simulation | Gazebo, Isaac Sim, Webots | After research phase |
| AI framework | PyTorch, JAX | After architecture decision |
| RL framework | Stable-Baselines3, RLlib | After research question defined |
| Mapping | Grid maps, occupancy maps, neural | After literature review |
| Multi-agent comm | ROS 2 DDS, custom | After architecture decision |

## Stack Principles
- Select based on research requirements, not technology hype
- ROS 2 is confirmed — everything else must justify its presence
- C++ where performance requires it, Python for logic and AI
- Simulation before hardware for algorithm validation

## Architecture Concept
```
Sensors
↓ Perception
↓ Localization / Mapping
↓ Environmental representation
↓ Decision-making / Learning  ← research focus
↓ Exploration target
↓ Motion planner
↓ Robot control
```