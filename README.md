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
* **Scientific Computing:** NumPy[cite: 1]
* **Visualization:** Matplotlib[cite: 1]

---

## 🚗 Simulation Environment Setup
The traffic network models a realistic highway infrastructure configured as follows[cite: 1]:

### 📐 Road Geometry
* **Freeway Sections (E0, E1):** 3 lanes in each direction with a speed limit of 13.89 m/s (50 km/h)[cite: 1].
  * **Edge E0:** 58.13 meters (connecting J0 to J1)[cite: 1].
  * **Edge E1:** 78.01 meters (continuation of the highway from J1 to J2)[cite: 1].
* **On-Ramp (E2):** A single lane entering from junction J3 to J1 with a length of 68.84 meters[cite: 1].
* **Controlled Junction (J1):** A traffic light intersection where highway and ramp flows interact[cite: 1].

### 📊 Traffic Demand
* **Highway Traffic Flow:** High volume consisting of 2400 vehicles per hour (vph)[cite: 1].
* **Ramp Traffic Flow:** Lower volume consisting of 200 vehicles per hour (vph)[cite: 1].
* **Simulation Duration:** 3600 seconds (1 hour) per episode[cite: 1].

---

## 🧠 Reinforcement Learning Reformulation

### 1. State Space
The environment state is captured as a vector containing[cite: 1]:
* **Highway Traffic Density:** Continuous value [0, 1] representing highway congestion[cite: 1].
* **Ramp Queue Length:** Continuous value [0, 1] tracking waiting vehicles on the ramp[cite: 1].
* **Traffic Light Phase:** Discrete variable representing the current state (Green, Yellow, or Red)[cite: 1].

### 2. Action Space
The discrete action space consists of 3 actions regulating the ramp traffic light[cite: 1]:
* **Action 0:** Green Light (Allow ramp vehicles to merge)[cite: 1].
* **Action 1:** Yellow Light (Transition phase)[cite: 1].
* **Action 2:** Red Light (Stop ramp traffic)[cite: 1].

### 3. Reward Functions

* **Q-Learning (Final Phase):** Evaluated via a scaled combination of traffic metrics[cite: 1]:
```text
R = 10 * (1 - highway_flow / max_highway_flow) + 5 * avg_speed - 5 * (ramp_queue / max_ramp_queue)
