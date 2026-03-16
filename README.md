# Hybrid RL-Enhanced Evolutionary Algorithm for FJSP

An end-to-end Python implementation of a custom Hybrid Artificial Intelligence architecture designed to solve the large-scale Flexible Job Shop Scheduling Problem (FJSP) for Industry 4.0 manufacturing. 

This system integrates an Evolutionary Algorithm (Genetic Algorithm) with a Deep Q-Network (DQN) Reinforcement Learning agent. By utilizing a stochastic simulation environment, the model optimizes complex scheduling tasks (20 Jobs, 10 Machines, 136 Operations) under uncertainty, yielding highly robust production schedules capable of withstanding real-world disruptions.

## Key Features
* **Online Hyper-heuristic Controller:** Uses a 4-layer PyTorch DQN to monitor population diversity and stagnation, dynamically selecting between Machine Crossover and Operation Crossover to prevent premature convergence.
* **Robust Optimization under Risk:** Replaces deterministic fitness functions with a stochastic decoder that injects a 5% random delay rate during training, forcing the evolution of resilient schedules with implicit buffer times.
* **Custom Two-Vector Encoding:** Implements a sophisticated chromosome structure natively handling both routing (Machine Sequence) and sequencing (Operation Sequence) without relying on restrictive static libraries.
* **High-Risk Stress Testing:** Demonstrates extreme stability, maintaining a 95.5% efficiency rate even when subjected to an extreme 30% uncertainty scenario.

## Architecture & Code Structure

The project is heavily modularized to separate the physical constraints of the factory from the logic of the AI optimizer.

* `main_rl_enhanced.py`: The conductor script. It initializes the population, runs the 100-generation hybrid optimization loop, trains the RL agent online via experience replay, and generates post-run visualizations (Gantt charts, convergence plots).
* `RL_Agent.py`: The "Brain." Contains the PyTorch Deep Q-Network. It takes a 3-variable state vector (Progress, Diversity, Stagnation) and outputs a crossover strategy decision using an epsilon-greedy policy.
* `GA.py`: The "Optimizer." Contains the dual-nature evolutionary operators. It executes Machine Crossover (for load balancing), Operation Crossover (for sequencing flow), and greedy mutation strategies.
* `Encode.py`: The "Initialization" module. Generates the initial chromosome population using a hybrid strategy (60% Global Selection, 20% Local Selection, 20% Random) to ensure both high initial quality and genetic diversity.
* `Decode.py`: The "Simulator." Translates abstract chromosome vectors into physical schedules. It calculates the Makespan (Cmax), actively searches for idle machine gaps to compress the schedule, and mathematically injects the stochastic risk factors.
* `Job.py` & `Machine.py`: The physical constraints layer. `Job.py` tracks operation progress to strictly enforce precedence constraints. `Machine.py` tracks timelines to enforce capacity constraints (preventing operational overlap).
* `new_Instance.py`: The problem generator. Creates the 20x10 FJSP testing environment, mapping 6-8 operations per job and assigning routing flexibility (3-5 capable machines per task).

## Installation & Usage

**Prerequisites:** Python 3.8+, PyTorch, NumPy, Matplotlib.

1. Clone the repository:
   ```bash
   git clone [https://github.com/yourusername/RL-Enhanced-FJSP.git](https://github.com/yourusername/RL-Enhanced-FJSP.git)
   cd RL-Enhanced-FJSP
