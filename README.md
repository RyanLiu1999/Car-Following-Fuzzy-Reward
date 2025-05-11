# Car-Following Fuzzy Reward

> Fuzzy logic-based reward shaping framework for reinforcement learning in car-following scenarios.

## 1. Introduction

This repository implements a fuzzy reward shaping mechanism for car-following tasks in reinforcement learning. By defining fuzzy sets for vehicle spacing and relative velocity, the framework generates smooth, expressive reward signals that encourage safe and efficient driving behavior.

Key features:
- Fuzzy reward functions based on distance-to-lead vehicle and relative speed
- Customizable membership functions and rule base
- Simulation environment compatible with the OpenAI Gym interface
- Jupyter notebooks demonstrating RL training, TTC-based trajectory generation, and MPC baseline

## 2. Repository Structure

Car-Following-Fuzzy-Reward/  
├── simulation_env.py               # Fuzzy reward simulation environment (Gym API)  
├── main.ipynb                      # Demonstration notebook: RL training with fuzzy reward  
├── TTC_generate_traj_origin.ipynb  # Generate trajectories based on Time-to-Collision  
├── MPC_acc.ipynb                   # Model Predictive Control baseline experiments  
├── trainSet.mat                    # Training dataset (car-following trajectories)  
├── testSet.mat                     # Test dataset  
├── requirements.txt                # Python dependencies  
└── README.md                       # This file

## 3. Installation

1. **Clone the repository**  
   ```bash
   git clone https://github.com/RyanLiu1999/Car-Following-Fuzzy-Reward.git
   cd Car-Following-Fuzzy-Reward
   ```

2. **Create a virtual environment and install dependencies**  
   ```bash
   python3 -m venv venv
   source venv/bin/activate   # macOS/Linux
   # venv\Scripts\activate  # Windows
   pip install -r requirements.txt
   ```

## 4. Usage

1. Launch Jupyter Notebook:  
   ```bash
   jupyter notebook
   ```
2. Open and run `main.ipynb` to train an RL agent using fuzzy reward shaping.  
3. Use `TTC_generate_traj_origin.ipynb` to generate reference trajectories via Time-to-Collision thresholds.  
4. Compare against the MPC baseline in `MPC_acc.ipynb`.

## 5. Fuzzy Reward Design

- **Inputs**:  
  - Distance to lead vehicle (d)  
  - Relative speed (Δv)  

- **Fuzzy sets for distance**:  
  - Close, Safe, Far  

- **Fuzzy sets for relative speed**:  
  - Closing, Stable, Opening  

- **Example rule base**:  
  1. IF d is Safe AND Δv is Stable THEN reward = High  
  2. IF d is Close AND Δv is Closing THEN reward = Low  
  3. IF d is Far AND Δv is Opening THEN reward = Medium  

Modify membership functions and rules in `simulation_env.py` to suit different driving scenarios.

## 6. Configuration

Adjust key parameters in `simulation_env.py` or the notebooks:

| Parameter                 | Description                                      | Default  |
|---------------------------|--------------------------------------------------|----------|
| `max_steps`               | Maximum steps per episode                        | 1000     |
| `distance_thresholds`     | [close, safe, far] membership thresholds (meters)| [5, 10]  |
| `velocity_thresholds`     | [closing, stable, opening] thresholds (m/s)      | [-2, 2]  |
| `fuzzy_rule_weights`      | Initial weights for each fuzzy rule              | [1,1,1]  |
| `learning_rate`           | RL agent learning rate                           | 1e-3     |

Refer to code comments for detailed parameter descriptions.

## 7. License

This project is licensed under the MIT License. See `LICENSE` for details.

## 8. Contact

Please open an issue on GitHub for questions or suggestions.

