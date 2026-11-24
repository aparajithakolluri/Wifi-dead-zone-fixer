# 📡 WiFi Dead Zone Fixer
### An ESP8266-Based Adaptive Reflector for Intelligent WiFi Signal Redirection

An adaptive WiFi signal redirection system that uses real-time Received Signal Strength Indicator (RSSI) feedback and a servo-controlled aluminum reflector to improve wireless signal reception in indoor dead zones.

This project demonstrates a low-cost, hardware-based approach inspired by **Reconfigurable Intelligent Surfaces (RIS)**, a promising technology for next-generation 6G wireless communication systems.

---

## 1. Project Overview

WiFi signals often experience weak coverage in certain indoor locations due to walls, furniture, obstacles and increasing distance from the router.

Conventional solutions such as WiFi extenders and mesh systems require additional networking hardware. This project explores an alternative approach: physically adjusting a reflector to redirect existing WiFi signals toward areas with poor reception.

The system uses two ESP8266 modules, a servo motor and an aluminum reflector. An RSSI-based feedback mechanism continuously evaluates signal strength and adjusts the reflector angle to search for an improved reception position.

**Core Concept:**

Measure → Analyze → Adjust → Re-measure → Optimize

## 2. Working Principle

The system consists of two ESP8266-based nodes.

1. **RSSI Measurement Node:** Positioned in the WiFi dead zone, it scans the router's WiFi signal and measures its RSSI.
2. **Controller Node:** Receives the RSSI measurements and controls the servo motor.
3. **Reflector Mechanism:** An aluminum reflector mounted on the servo changes its orientation to redirect incoming WiFi energy.
4. **Optimization Algorithm:** A hill-climbing approach evaluates RSSI changes and searches for an angle that provides improved signal strength.

The process repeats until the system identifies a suitable reflector orientation.

### System Block Diagram

```text
       WiFi Router
            |
            | 2.4 GHz WiFi Signal
            v
    Aluminum Reflector
      (Servo Mounted)
            |
            v
      WiFi Dead Zone
            |
            v
   ESP8266 - Node 1
    RSSI Measurement
            |
            | RSSI Feedback
            v
   ESP8266 - Node 2
    Control Algorithm
            |
            v
       Servo Motor
            |
            v
   Reflector Adjustment
            |
            └──── Feedback Loop
```

## 3. Hardware Requirements

| Component | Quantity | Function |
|---|---:|---|
| ESP8266 NodeMCU | 2 | RSSI measurement and system control |
| Servo Motor | 1 | Controls reflector orientation |
| Aluminum Reflector | 1 | Reflects WiFi radio waves |
| Jumper Wires | As required | Hardware connections |
| External Power Supply | As required | Powers the servo and controller |

*Note: Update the component models, reflector dimensions and power specifications according to the hardware actually used.*

## 4. Software Requirements

| Software / Technology | Purpose |
|---|---|
| Arduino IDE | Firmware development |
| Embedded C/C++ | Programming |
| ESP8266 WiFi Library | WiFi scanning and RSSI measurement |
| Servo Library | Servo motor control |
| Serial Communication | Debugging and monitoring |

### Firmware Modules

**Node 1 – RSSI Measurement**
- Scans available WiFi networks.
- Identifies the target router.
- Measures received signal strength in dBm.
- Transmits RSSI readings to the controller node.

**Node 2 – Servo Control**
- Receives RSSI feedback.
- Implements the hill-climbing optimization algorithm.
- Adjusts the servo motor position.
- Evaluates changes in signal strength to determine the next movement.

## 5. Optimization Algorithm – Hill Climbing

Hill climbing is a local optimization technique that searches for an improved solution by evaluating neighboring positions.

In this project, the reflector angle is treated as the optimization parameter, while RSSI is the objective function.

**Algorithm:**

1. Initialize the reflector at a starting angle.
2. Measure the RSSI at the receiver.
3. Change the reflector angle by a predefined step.
4. Measure RSSI again.
5. Compare the new RSSI with the previous measurement.
6. If signal strength improves, continue in that direction.
7. Otherwise, reverse the search direction.
8. Repeat until a suitable reflector angle is identified.

The objective is to maximize received signal strength.

\[
\theta_{\text{optimal}} = \arg\max_{\theta} RSSI(\theta)
\]

## 6. Experimental Results

The performance of the system can be evaluated by comparing received signal strength under different reflector conditions.

| Test Condition | RSSI (dBm) |
|---|---|
| Without reflector | To be measured |
| Reflector at fixed angle | To be measured |
| Reflector after optimization | To be measured |

**Experimental Setup:**
- Operating frequency: 2.4 GHz
- Communication technology: WiFi (IEEE 802.11)
- Receiver location: WiFi dead zone
- Optimization technique: Hill climbing
- Reflector angle: To be measured
- Router-to-receiver distance: To be measured

*Experimental values will be added after hardware testing.*

## 7. Connection to RIS and 6G Technology

Reconfigurable Intelligent Surfaces (RIS) are emerging technologies designed to control the propagation of electromagnetic waves by manipulating their reflection characteristics.

This project demonstrates a simplified mechanical analogy of the RIS concept.

| Parameter | WiFi Dead Zone Fixer | Real RIS |
|---|---|---|
| Reflecting structure | Aluminum reflector | Array of engineered unit cells |
| Signal control | Mechanical steering | Electronic phase control |
| Control mechanism | Servo motor | PIN diodes / Varactors |
| Feedback | RSSI | CSI / Channel estimation |
| Optimization | Hill climbing | Beamforming / Intelligent optimization |

Although this prototype does not implement a true RIS, it demonstrates the fundamental concept of feedback-based wireless propagation optimization.

## 8. Applications

- Indoor WiFi coverage improvement research
- Wireless signal propagation experiments
- Smart antenna and reflector systems
- Embedded wireless communication projects
- RIS-inspired experimental prototypes
- RF and antenna engineering demonstrations

## 9. Limitations

- Uses mechanical reflection rather than electronic phase control.
- Designed for 2.4 GHz WiFi experiments.
- RSSI measurements can fluctuate due to multipath propagation and environmental interference.
- Hill climbing may converge to a local optimum.
- Performance depends on reflector geometry, placement and surrounding obstacles.
- A single reflector does not provide the independent phase control available in a true RIS.

## 10. Future Enhancements

- Implement dual-axis reflector steering.
- Explore multiple reflector geometries.
- Introduce advanced optimization algorithms.
- Develop electronically tunable reflecting elements using PIN diodes or varactors.
- Investigate operation at 5 GHz.
- Implement RSSI data logging and signal-strength visualization.
- Explore multi-user wireless coverage optimization.

## 11. Repository Structure

```text
WiFi-Dead-Zone-Fixer/
│
├── node1_rssi/
│   └── RSSI measurement firmware
│
├── node2_servo/
│   └── Servo control and optimization firmware
│
├── docs/
│   ├── images/
│   ├── wiring.png
│   ├── block_diagram.png
│   └── demo.mp4
│
└── README.md
```

## 12. Technologies Used

`ESP8266` `Arduino IDE` `Embedded C++` `WiFi` `RSSI` `Servo Motor` `Wireless Communication` `RF Engineering` `Antenna Systems` `RIS` `6G Technology`

## 13. Author

**K. V. S. L. J. Aparajitha**

B.Tech – Electronics and Communication Engineering

Vignan's Institute of Engineering for Women, Visakhapatnam

GitHub: [@aparajithakolluri](https://github.com/aparajithakolluri)

---

*This project explores the intersection of embedded systems, RF engineering, wireless communication and emerging RIS-inspired technologies.*
