# Reinforcement Learning for Highway Ramp Metering

An implementation of Reinforcement Learning (RL) algorithms to optimize traffic flow and control ramp metering at highway intersections using the SUMO (Simulation of Urban MObility) simulator.

---

## 👥 Authors
* **AMIRA Ramzi** (3cs2)
* **DRAA Abdel-Illah** (3cs1)

---

## 📝 Project Overview
This project addresses the challenge of traffic congestion at highway merging zones. By utilizing Reinforcement Learning, an intelligent agent learns to dynamically control traffic light phases at an on-ramp junction. The core objective is to maximize vehicle speed and highway traffic flow while minimizing queue accumulation on the ramp.

The project evaluates and compares two distinct RL approaches across multiple experimental phases:
1. **Tabular Q-Learning** (tested across 5 progressive optimization phases)
2. **Deep Q-Network (DQN)** (leveraging deep neural networks for continuous state approximation)

---

## 🛠️ Technologies & Frameworks
* **Traffic Simulation:** SUMO (Simulation of Urban MObility)
* **Control Interface:** TraCI (Traffic Control Interface)
* **Deep Learning:** TensorFlow / Keras
* **Scientific Computing:** NumPy
* **Visualization:** Matplotlib

---

## 🚗 Simulation Environment Setup
The traffic network models a realistic highway infrastructure configured as follows:

### 📐 Road Geometry
* **Freeway Sections (E0, E1):** 3 lanes in each direction with a speed limit of 13.89 m/s (50 km/h).
  * **Edge E0:** 58.13 meters (connecting J0 to J1).
  * **Edge E1:** 78.01 meters (continuation of the highway from J1 to J2).
* **On-Ramp (E2):** A single lane entering from junction J3 to J1 with a length of 68.84 meters.
* **Controlled Junction (J1):** A traffic light intersection where highway and ramp flows interact.

### 📊 Traffic Demand
* **Highway Traffic Flow:** High volume consisting of 2400 vehicles per hour (vph).
* **Ramp Traffic Flow:** Lower volume consisting of 200 vehicles per hour (vph).
* **Simulation Duration:** 3600 seconds (1 hour) per episode.

---

## 🧠 Reinforcement Learning Reformulation

### 1. State Space
The environment state is captured as a vector containing:
* **Highway Traffic Density:** Continuous value [0, 1] representing highway congestion.
* **Ramp Queue Length:** Continuous value [0, 1] tracking waiting vehicles on the ramp.
* **Traffic Light Phase:** Discrete variable representing the current state (Green, Yellow, or Red).

### 2. Action Space
The discrete action space consists of 3 actions regulating the ramp traffic light:
* **Action 0:** Green Light (Allow ramp vehicles to merge).
* **Action 1:** Yellow Light (Transition phase).
* **Action 2:** Red Light (Stop ramp traffic).

### 3. Reward Functions

* **Q-Learning (Final Phase):** Evaluated via a scaled combination of traffic metrics:
```text
R = 10 * (1 - highway_flow / max_highway_flow) + 5 * avg_speed - 5 * (ramp_queue / max_ramp_queue)



├── Project RL/
│   ├── code/
│   │   ├── Deep Q Learning.ipynb         # DQN agent architecture and training loop
│   │   ├── Q Learning test 1.ipynb       # Initial Q-learning experimental phase
│   │   ├── Q Learning test 2.ipynb       # Q-learning phase with extended episodes (200)
│   │   ├── Q Learning test 3.ipynb       # Q-learning phase with log-reward scaling
│   │   ├── Q Learning test 4.ipynb       # Q-learning phase with high exploration rate
│   │   ├── Q Learning test 5 Final.ipynb # Optimized Q-learning model with stable metrics
│   │   ├── test1.add                     # SUMO additional infrastructure elements
│   │   ├── test1.net                     # SUMO road network geometry
│   │   ├── test1.rou                     # SUMO traffic demand and route specifications
│   │   └── test1.sumocfg                 # SUMO simulation main configuration file
│   └── Report.pdf                        # Academic project report (PDF version)
├── Report.docx                           # Academic project report (Word version)
└── README.md                             # Repository documentation
