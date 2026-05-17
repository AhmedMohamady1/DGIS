<div align="center">

<br/>

```
██████╗  ██████╗ ██╗███████╗
██╔══██╗██╔════╝ ██║██╔════╝
██║  ██║██║  ███╗██║███████╗
██║  ██║██║   ██║██║╚════██║
██████╔╝╚██████╔╝██║███████║
╚═════╝  ╚═════╝ ╚═╝╚══════╝
```

**Drone Geographical Information System**

*Autonomous drone swarms for large-scale wildlife and environmental monitoring*

[![Simulation](https://img.shields.io/badge/Unity-6.2_LTS-black?logo=unity)](https://github.com/your-org/dgis-simulation)
[![ML Models](https://img.shields.io/badge/YOLO-v26-purple?logo=python)](https://github.com/AhmedMohamady1/dgis-ml-models)
[![Mobile](https://img.shields.io/badge/Android-Kotlin-green?logo=android)](https://github.com/your-org/dgis-mobile)
[![Hardware](https://img.shields.io/badge/ESP32-PlatformIO-red?logo=espressif)](https://github.com/your-org/dgis-hardware)
[![Analytics](https://img.shields.io/badge/Dashboard-React-blue?logo=react)](https://github.com/your-org/dgis-analytics)

<br/>

</div>

---

## What is DGIS?

DGIS is an autonomous multi-drone system that surveys remote ecosystems — detecting wildlife, mapping terrain in 3D, and generating environmental reports — without human intervention.

Traditional ground surveys take months. DGIS deploys a swarm of UAVs that navigate autonomously using Reinforcement Learning, classify flora and fauna in real time using YOLO-based computer vision, reconstruct terrain as a 3D point cloud via LiDAR raycasting, and deliver a complete analytical report at mission end.

The system is paired with a quadruped robot (spider-inspired, 12-servo, IK-controlled) for terrain that drones can't reach, with an Android smartphone acting as its onboard brain.

---

## System Architecture

```
┌────────────────────────────────────────────────────────────────┐
│                        DGIS Ecosystem                          │
│                                                                │
│  ┌──────────────────┐        ┌──────────────────────────────┐  │
│  │  dgis-simulation │        │       dgis-ml-models         │   │
│  │                  │        │                              │   │
│  │  Unity 3D        │◄───────│  YOLO Training (sim)         │   │  
│  │  RL Navigation   │        │  YOLO Training (mobile)      │   │
│  │  LiDAR / HUD     │        │  .onnx exports               │   │
│  │  5 Biome Scenes  │        │  Jupyter Notebooks           │   │
│  └────────┬─────────┘        └──────────────────────────────┘  │
│           │ mission data                                       │
│           ▼                                                    │
│  ┌──────────────────┐        ┌──────────────────────────────┐  │
│  │  dgis-analytics  │        │       dgis-mobile            │  │
│  │                  │        │                              │  │
│  │  Post-mission    │        │  Android App                 │  │
│  │  Dashboard       │        │  Camera + IMU + GPS          │  │
│  │  Species Reports │        │  ESP32 Communication         │  │
│  │  Density Maps    │        │  On-device YOLO inference    │  │
│  └──────────────────┘        └──────────┬───────────────────┘  │
│                                         │ USB / BLE            │
│                              ┌──────────▼───────────────────┐  │
│                              │      dgis-hardware           │  │
│                              │                              │  │
│                              │  ESP32 Firmware              │  │
│                              │  Inverse Kinematics (IK)     │  │
│                              │  12-Servo Quadruped Control  │  │
│                              └──────────────────────────────┘  │
└────────────────────────────────────────────────────────────────┘
```

---

## Repositories

| Repo | Description | Stack |
|------|-------------|-------|
| [dgis-simulation](https://github.com/your-org/dgis-simulation) | Unity 3D simulation — 7 biome environments, drone flight, RL navigation, LiDAR, HUD, data generation pipeline | Unity 2022.3 LTS, C#, ML-Agents, URP |
| [dgis-ml-models](https://github.com/AhmedMohamady1/dgis-ml-models) | YOLO model training for sim and mobile, dataset configs, `.onnx` exports, training notebooks | Python, YOLOv8, PyTorch, Jupyter |
| [dgis-mobile](https://github.com/your-org/dgis-mobile) | Android app — on-device YOLO inference, IMU/GPS sensing, ESP32 communication, robot control | Kotlin, Android SDK |
| [dgis-hardware](https://github.com/your-org/dgis-hardware) | ESP32 firmware — quadruped inverse kinematics, servo control, telnet bridge | C/C++, PlatformIO |
| [dgis-analytics](https://github.com/your-org/dgis-analytics) | Post-mission analytics dashboard — species density, distribution maps, automated report generation | React, SQLite |

---

## Getting Started

### Clone everything

```bash
git clone https://github.com/AhmedMohamady1/DGIS
cd DGIS
bash scripts/clone-all.sh
```

Or clone individual components:

```bash
# Simulation only
git clone https://github.com/your-org/dgis-simulation

# ML models only
git clone https://github.com/AhmedMohamady1/dgis-ml-models

# Mobile app only
git clone https://github.com/your-org/dgis-mobile

# Hardware / ESP32 only
git clone https://github.com/your-org/dgis-hardware

# Analytics dashboard only
git clone https://github.com/your-org/dgis-analytics
```

### Prerequisites by component

| Component | Requirements |
|-----------|-------------|
| Simulation | Unity 6.2 LTS |
| ML Models | Python 3.10+, `pip install ultralytics torch` |
| Mobile | Android Studio, Android SDK 26+ |
| Hardware | PlatformIO, ESP32 board support |
| Analytics | Node.js 18+, npm |

---

## Project Structure (this repo)

```
dgis/
├── README.md               ← You are here
├── ARCHITECTURE.md         ← Deep-dive on component communication
├── docs/
│   ├── DGIS_Documentation.pdf    ← Full graduation project doc
│   ├── ERD.png                   ← Entity-Relationship Diagram
│   ├── DFD.png                   ← Data Flow Diagrams
│   └── sequence_diagrams/
├── scripts/
│   └── clone-all.sh        ← Clone all sub-repos at once
└── shared/
    └── db_schema.sql       ← SQLite schema shared by simulation & analytics
```

---

## Key Features

- **Autonomous Navigation** — Reinforcement Learning (ML-Agents) with A* pathfinding for obstacle avoidance across 7 distinct biome environments
- **Computer Vision** — Dual YOLO models: one trained on simulation-generated synthetic data, one optimized for mobile on-device inference
- **LiDAR & 3D Reconstruction** — Raycasting-based depth sensing that builds georeferenced 3D point clouds of surveyed terrain
- **Swarm Coordination** — Multi-agent coverage algorithm to maximize area efficiency across drone units
- **Quadruped Robot** — 12-servo, IK-controlled spider robot with smartphone as onboard CPU for terrain unreachable by drones
- **Automated Reporting** — Post-mission analytics: species density estimation, vegetation distribution maps, full environmental report

---

## Team

**Faculty of Computing and Data Sciences — Alexandria University**
Graduation Project · Fall 2025 · Team 20

| Name |
|------|
| Ahmed Mohamed Mahmoud |
| Fares Ahmed Abu El-Fotoh |
| Mohammed Mahmoud Naeem |
| Ahmed Emad Abdelfattah |
| Omar Hafez Mammoun |
| Omar Ehab Mohamed |
| Al-Hussain Yasser Ibrahim |

**Supervisor:** Dr. Mahmoud Gamal

---

## License

MIT — see [LICENSE](LICENSE) for details.
