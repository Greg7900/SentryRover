# 🚀 Mobile Rover with Intelligent Pan & Tilt Turret

## 📌 Overview

This project aims to design and build a **mobile rover** capable of carrying a payload and moving at high speed over various terrains, equipped with a **motorized pan & tilt turret** for target detection and tracking using **computer vision**.

The system is designed to be **modular**, allowing for the integration of different sensors, cameras, and processing units.  
A **NVIDIA Jetson Orin Nano Super Developer Kit** handles vision and decision-making, while dedicated electronics drive the motors and actuators.

---

## 🛠️ Main Components

### 🔹 Rover Chassis
- **4x 90W Brushless DC Motors** with 5.36:1 planetary gearbox (1.38 Nm, 560 RPM)
- **16 cm diameter wheels**
- **Motor drivers**: 4x PWM/Direction compatible drivers
- **Battery**: 6S LiPo, capacity depending on desired runtime
- **Structure**: Aluminum profiles and 3D printed mounts
- **Low-level control electronics**: Arduino (or equivalent) for motor control

### 🔹 Pan & Tilt Turret
- **Pan**: NEMA 23 90W servomotor (0.3 Nm nominal, 0.8 Nm peak, 3000 RPM) with GT2 belt reduction (1:10 ratio)
- **Tilt**: Same or smaller servomotor depending on requirements
- **Transmission**: Timing belts and machined pulleys
- **Platform**: Camera mount + mechanical stabilization

### 🔹 Vision & Processing
- **Main board**: NVIDIA Jetson Orin Nano Super Developer Kit (JetPack 6)
- **Camera**: Arducam USB Global Shutter or Logitech Brio (depending on use case)
- **Algorithms**: YOLOv8n optimized with TensorRT for real-time detection (~40–50 FPS)
- **ROS2**: Node management, navigation, and vision
- **Simulation**: Gazebo for virtual testing

---

## ⚙️ Performance Goals

### Rover
- **Target top speed**: 5 m/s
- **Minimum payload**: 15 kg
- **Target acceleration**:  
  - 1 m/s² with max load  
  - 3 m/s² with reduced load  
- **Motor torque**: 1.38 Nm nominal  
- **Estimated rover weight (without payload)**: ~12–14 kg

### Turret
- **PAN rotation**: 360° in 0.2 s
- **TILT rotation**: Fast but less critical
- **Required PAN torque**: ~4.4 Nm for a 10 kg platform
- **Target accuracy**: < 0.5° error

---

## 🔌 Component Integration

```plaintext
[Jetson Orin Nano]
       │
       ├── (USB) → Global Shutter Camera
       ├── (Ethernet/Wi-Fi) → Control interface
       ├── (UART/I²C) → Arduino / Low-level controller
       │
[Arduino / Motor controller]
       ├── PWM/Dir → Rover motor drivers
       ├── PWM/Dir → Turret motor drivers
       └── Sensors (IMU, encoders, etc.)
