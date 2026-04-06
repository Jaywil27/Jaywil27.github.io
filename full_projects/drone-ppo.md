---
layout: page
title: "Creating a self-hovering drone using PPO and neural networks"
permalink: /full_projects/drone-ppo/
---

# PPO-Based Quadcopter Drone Project

---

## 1. Introduction

### 1.1 Purpose of the Project

The primary goal of this project was to build a quadrotor drone as a personal learning exercise. The focus was on improving skills across multiple domains, including:

- Artificial Intelligence
- Robotics
- Reinforcement Learning
- Electronics
- Mechanical Design
- 3D Printing

Rather than validating a specific hypothesis or contributing to formal research, the project was designed as a hands-on exploration. Success was defined by:

- Successfully building the drone
- Achieving stable hover (real or simulated)

Additionally, the project served as a way to learn and integrate complex tools and workflows across hardware and software systems. :contentReference[oaicite:0]{index=0}

---

### 1.2 Project Overview

This project implements a quadrotor drone controlled by a **PPO (Proximal Policy Optimization) actor-critic model**.

**Key characteristics:**
- Target hover height: **1 meter**
- No PID controller used
- Direct thrust control via neural network
- Fully trained in simulation

**Performance summary:**

| Metric                     | Value            |
|--------------------------|------------------|
| Stable hover range       | 0.90 – 0.99 m    |
| Disturbance recovery     | ~2° – 5° optimal |
| Max recovery             | ~9–10°           |
| Training environment     | Simulation only  |

The system achieved partial stabilization, capable of maintaining hover but not fully robust to large disturbances. :contentReference[oaicite:1]{index=1}

---

### 1.3 Objectives and Goals

The main objectives of the project were:

- Build a functional quadrotor drone
- Develop a reinforcement learning controller for hover
- Learn complex interdisciplinary skills

**Design philosophy:**
- Prioritize learning over simplicity
- Avoid traditional PID controllers intentionally
- Build as much of the system from scratch as possible

---

### 1.4 Scope of the Report

This report covers:

- System architecture
- Mechanical design
- Electrical system
- Flight controller and sensors
- Reinforcement learning pipeline
- Testing and validation

Due to limited real-world testing, the focus is on implementation and observed behavior rather than formal validation.

---

### 1.5 Background on Drone Technology

Traditional drones rely on **PID controllers** for stabilization. These are:

- Easier to implement
- More robust
- Industry standard

This project instead uses reinforcement learning to directly map observations → motor thrust.

**Why PPO?**
- Prior familiarity
- Proven use in autonomous systems
- Stability compared to other RL algorithms

---

## 2. System Overview

### 2.1 System Components

**Hardware:**

| Component        | Description                      |
|-----------------|----------------------------------|
| Frame           | 3D printed PLA                   |
| Motors          | 1000 KV                          |
| Propellers      | 10 inch                          |
| ESC             | 45A Hacker ESC                   |
| Battery         | 11.1V 3S 2000mAh                |
| Controller      | ESP32                            |
| Sensors         | IMU + ToF                        |

**Software:**

- Isaac Lab / Isaac Sim
- PhysX physics engine
- PPO training via SKRL
- Custom RL environment

---

### 2.2 System Architecture

The architecture can be divided into two major domains:

1. **Simulation and training architecture**
2. **Real-world inference and control architecture**

#### Simulation and Training Architecture

The simulated system included:

- Physics simulation layer
- Robot articulation and drone model
- Reinforcement learning environment
- PPO policy optimization and inference

#### Real-World Architecture

The real-world system included:

- Sensor data collection
- Filtering and normalization
- External inference on a computer
- Command transmission
- DShot motor control through the ESP32 and ESC

This separation allowed the drone to be trained in simulation while still supporting later physical deployment with real sensors and hardware control. :contentReference[oaicite:11]{index=11}

---
**Drone Flying in Simulation:**

![Drone Demo](/assets/images/Drone-hover-isaacsim.gif)


---

### 2.3 Design Requirements

- Must hover at **1 meter**
- Must be physically buildable
- Must integrate RL control

**Constraints:**
- Limited indoor testing space
- Safety concerns (no prop guards)
- Sensor noise and drift
- Hardware limitations (ESP32)

---

### 2.4 Performance Targets

| Metric                     | Value              |
|--------------------------|--------------------|
| Hover height             | 1 m                |
| Stable range             | 0.90 – 0.99 m      |
| Avg thrust               | 3–4 N              |
| Max thrust               | 7.12 N             |
| Flight time              | ~15 minutes        |
| Disturbance recovery     | 2–5° (best)        |

---

## 3. Design Process

### 3.1 Methodology

The design process was highly iterative and included:

- CAD redesign cycles
- Reward tuning
- Sensor calibration
- Simulation adjustments

---

### 3.2 Tradeoffs

| Decision                | Tradeoff |
|------------------------|---------|
| RL vs PID              | Harder but more educational |
| ESP32 vs flight controller | Simpler but less optimal |
| Simulation realism     | Faster dev vs lower accuracy |

---

### 3.3 Final Design

The final system includes:

- PPO actor-critic controller
- Isaac Lab simulation training
- ESP32-based control system
- 3D printed frame

---

## 4. Mechanical Design

### 4.1 Key Dimensions

| Feature           | Value        |
|------------------|-------------|
| Wing length      | 12.565 cm   |
| Prop size        | 10 inch     |
| Body height      | 3.786 cm    |
| Weight           | 1.585 lbs   |

---

### 4.2 Structural Issues

Main failure points:
- Wing-to-body joints
- Motor mount alignment

---

## 5. Electrical System


### 5.1 Power System

| Component   | Value              |
|------------|--------------------|
| Battery    | 11.1V 3S 2000mAh   |
| Flight time| ~15 minutes        |

---

## 6. Flight Controller and Sensors

### 6.1 Controller

- ESP32 used for:
  - DShot output
  - Sensor integration
  - Emergency stop

---

### 6.2 Sensors

| Sensor | Purpose |
|--------|--------|
| IMU    | Orientation + angular velocity |
| ToF    | Height measurement |

---

### 6.3 Sensor Challenges

- Drift issues
- Noise handling
- Orientation mismatch (major bug)

---

## 7. Software and Control System

### 7.1 Control Strategy

- PPO actor-critic model
- Continuous action space (4 motors)

---

### 7.2 Network Architecture

| Layer | Size |
|------|-----|
| Input | state |
| Hidden | 512 → 256 |
| Output | 4 (motors) |

---

### 7.3 Training Details

| Parameter        | Value           |
|-----------------|-----------------|
| Steps           | 20k – 50k       |
| Convergence     | ~7k steps       |
| Learning rate   | 1e-4            |
| Batch size      | ~1000           |

---

## 9. Testing and Validation

### 9.1 Performance Metrics

| Metric                 | Value        |
|----------------------|-------------|
| Hover target         | 1 m         |
| Stable range         | 0.90–0.99 m |
| Max tilt recovery    | ~9°         |
| Disturbance range    | 2–5°        |
| Avg thrust           | 3–4 N       |

---

### 9.2 Testing Limitations

- Indoor only testing
- No prop guards
- Limited real-world validation

---

## 10. Conclusion

This project demonstrates that reinforcement learning can be used to control a quadrotor drone for hover tasks, though with limited robustness.

While not as practical as PID-based systems, the project successfully achieved its goal of:

- Building a working drone
- Applying RL to a real-world control problem
- Developing interdisciplinary engineering skills