# IoT Smart Home Sensor Network — WSN Simulation

![Cisco Packet Tracer](https://img.shields.io/badge/Cisco%20Packet%20Tracer-8.2.2-blue?style=flat-square&logo=cisco)
![IoT](https://img.shields.io/badge/Domain-IoT%20%7C%20Networking-green?style=flat-square)
![PDR](https://img.shields.io/badge/Packet%20Delivery%20Ratio-100%25-brightgreen?style=flat-square)
![Delay](https://img.shields.io/badge/End--to--End%20Delay-20.5ms-orange?style=flat-square)
![License](https://img.shields.io/badge/License-Academic-lightgrey?style=flat-square)

A fully simulated **IoT-based Smart Home Sensor Network** built in Cisco Packet Tracer. This project covers end-to-end network design, wireless security configuration, IoT device registration, event-driven automation, and quantitative performance analysis.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Network Architecture](#network-architecture)
- [Components Used](#components-used)
- [Wireless Security](#wireless-security)
- [Automation Rules](#automation-rules)
- [Performance Analysis](#performance-analysis)
- [Repository Structure](#repository-structure)
- [Getting Started](#getting-started)
- [Key Learnings](#key-learnings)
- [Author](#author)

---

## Project Overview

This simulation models a **smart home environment** where sensors continuously monitor environmental parameters and actuators respond intelligently through pre-configured automation logic — all managed via a central IoT Server over a secure Wi-Fi network.

**What this project demonstrates:**
- Designing a scalable IoT network from scratch in Cisco Packet Tracer
- Configuring DHCP, static IPs, and wireless security (WPA2-PSK/AES)
- Registering and managing 7 heterogeneous IoT devices on a central server
- Writing event-driven automation rules for real-time device control
- Measuring and interpreting PDR, Throughput, and End-to-End Delay

---

## Network Architecture

```
┌─────────────────────────────────────────────────────────┐
│                     Wired Backbone                      │
│                                                         │
│   ┌────────────┐      ┌──────────────┐                  │
│   │ IoT Server │──────│    Switch    │                  │
│   │ 192.168.0.10│     │  2960-24TT   │──── PC           │
│   └────────────┘      └──────┬───────┘                  │
│                              │                          │
│                     ┌────────┴────────┐                 │
│                     │ Wireless Router │                 │
│                     │   WRT300N       │                 │
│                     │  192.168.0.1    │                 │
│                     └────────┬────────┘                 │
└──────────────────────────────┼──────────────────────────┘
                               │  Wi-Fi · SSID: IoT_Wireless
         ┌──────────┬──────────┼──────────┬──────────┬────────────┐
         │          │          │          │          │            │
   Motion Sensor  Door      Temp       Smart     Smart      Smoke +
                 Sensor    Sensor      Light      Fan       Camera +
                                                           Smartphone
                                    (All via DHCP: 192.168.0.100–149)
```

**Topology:** Star — Switch as central hub, Router as wireless access point.

| Device | IP Address | Type |
|---|---|---|
| IoT Server | 192.168.0.10 | Static |
| Wireless Router | 192.168.0.1 | Static (Gateway) |
| All IoT Devices | 192.168.0.100 – 149 | DHCP |

---

## Components Used

| # | Device | Model | Function |
|---|---|---|---|
| 1 | IoT Server | Server-PT | Central hub: registration, automation, data |
| 2 | Network Switch | Cisco 2960-24TT | Wired LAN backbone |
| 3 | Wireless Router | WRT300N | Wi-Fi access for all IoT devices |
| 4 | Motion Sensor | IoT-PT | Detects human presence |
| 5 | Door Sensor | IoT-PT | Monitors lock / unlock status |
| 6 | Temperature Sensor | IoT-PT | Ambient temperature monitoring |
| 7 | Smart Light | IoT-PT | Dimmable lighting actuator |
| 8 | Smart Fan | IoT-PT | Variable-speed fan actuator |
| 9 | Smoke Detector | IoT-PT | Fire and smoke hazard detection |
| 10 | Security Camera | IoT-PT (Webcam) | Visual surveillance |
| 11 | Smartphone | SMARTPHONE-PT | Remote monitoring and control |

---

## Wireless Security

| Parameter | Value |
|---|---|
| SSID | IoT_Wireless |
| Security Mode | WPA2 Personal (PSK) |
| Encryption | AES |
| Channel | 1 — 2.412 GHz |
| Key Renewal | 3600 seconds |

All IoT devices authenticate using WPA2-PSK before obtaining a DHCP lease, ensuring only registered devices can join the network.

---

## Automation Rules

Six event-driven rules configured on the IoT Server enable autonomous smart home behavior:

| # | Rule | Trigger Condition | Actions |
|---|---|---|---|
| 1 | Door Open → Lights & Fan ON | Door Sensor = Unlock | Light → ON, Fan → HIGH |
| 2 | Door Close → Lights & Fan OFF | Door Sensor = Lock | Light → OFF, Fan → OFF |
| 3 | Motion Detected → Light ON | Motion Sensor = true | Light → ON |
| 4 | No Motion → Light OFF | Motion Sensor = false | Light → OFF |
| 5 | High Temperature → Fan ON | Temperature > 25.0 °C | Fan → HIGH |
| 6 | Normal Temperature → Fan LOW | Temperature < 25.0 °C | Fan → LOW |

These rules demonstrate **event-driven IoT architecture** — actuators respond to sensor states in real time without any manual intervention.

---

## Performance Analysis

Network performance was evaluated using a 100-packet ICMP ping test from the PC to the Smartphone (`192.168.0.115`).

### 1. Packet Delivery Ratio (PDR)

Measures network reliability — the fraction of sent packets successfully received.

```
PDR = (Packets Received / Packets Sent) × 100
    = (100 / 100) × 100
    = 100%
```

> Zero packet loss observed across all 100 transmitted packets.

---

### 2. Throughput

Measures the effective data transmission rate during the test.

```
Total Data  = 100 packets × 32 bytes = 3,200 bytes = 25,600 bits
Duration    = 4.1 seconds
Throughput  = 25,600 / 4.1 ≈ 6,243.9 bps ≈ 6.24 kbps
```

> This reflects ICMP test traffic only. The WRT300N supports up to 54 Mbps (802.11g).

---

### 3. End-to-End Delay

Measures the one-way packet travel time from source to destination.

```
Average RTT      = 41 ms
End-to-End Delay = RTT / 2 = 20.5 ms
```

| Metric | Value |
|---|---|
| Minimum RTT | 11 ms |
| Maximum RTT | 159 ms |
| Average RTT | 41 ms |
| **End-to-End Delay** | **20.5 ms** |

> Smart home applications typically require latency under 100–500 ms. At 20.5 ms, this network is well within acceptable bounds.

---

### Results Summary

| Metric | Result | Benchmark | Status |
|---|---|---|---|
| Packet Delivery Ratio | 100% | > 95% | ✅ Excellent |
| Throughput | 6.24 kbps | Adequate for IoT sensor traffic | ✅ Pass |
| End-to-End Delay | 20.5 ms | < 100 ms for smart home | ✅ Excellent |

---

## Repository Structure

```
IoT-Smart-Home-WSN-Simulation/
│
├── README.md
│
├── simulation/
│   └── IoT_Smart_Home_Sensor_Network_WSN_Simulation.pkt
│
└── screenshots/
    ├── 01_initial_topology.png
    ├── 02_pc_ip_config.png
    ├── 03_router_dhcp_setup.png
    ├── 04_wireless_settings.png
    ├── 05_wireless_security_wpa2.png
    ├── 06_iot_server_ip_config.png
    ├── 07_iot_server_gateway.png
    ├── 08_registration_service.png
    ├── 09_temp_sensor_registration.png
    ├── 10_all_devices_registered.png
    ├── 11_device_controls.png
    ├── 12_complete_topology.png
    ├── 13_automation_rules.png
    ├── 14_door_sensor_control.png
    ├── 15_smartphone_config.png
    ├── 16_ping_phase1.png
    ├── 17_ping_phase2.png
    ├── 18_ping_phase3.png
    └── 19_ping_statistics.png
```

---

## Getting Started

### Prerequisites

- [Cisco Packet Tracer 8.2.2+](https://www.netacad.com/courses/packet-tracer) — free with a Cisco NetAcad account

### Steps

**1. Clone the repository**
```bash
git clone https://github.com/YOUR_USERNAME/IoT-Smart-Home-WSN-Simulation.git
cd IoT-Smart-Home-WSN-Simulation
```

**2. Open the simulation**
- Launch Cisco Packet Tracer
- File → Open → `simulation/IoT_Smart_Home_Sensor_Network_WSN_Simulation.pkt`

**3. Explore registered devices**
- Click **PC** → Desktop → Web Browser → `http://192.168.0.10`
- Login: `admin / admin`
- View all 7 registered IoT devices and configured automation rules

**4. Test automation**
- Click the **Door Sensor** → toggle Lock / Unlock → watch Smart Light and Fan respond
- Click the **Temperature Sensor** → set value above 25 °C → Fan activates automatically

**5. Run the performance test**
- Click **PC** → Desktop → Command Prompt
```
ping 192.168.0.115 -n 100
```
- Observe PDR, RTT statistics, and calculate throughput

---

## Key Learnings

- **IoT Network Design** — Building a complete sensor-actuator network with a central management server
- **Wireless Security** — Implementing WPA2-PSK with AES encryption for device authentication
- **DHCP vs Static IP** — Choosing appropriate addressing strategies for different device roles
- **Event-Driven Automation** — Designing condition-action rules for autonomous device behaviour
- **Network Performance Analysis** — Measuring PDR, Throughput, and End-to-End Delay from empirical test data
- **Wireless Sensor Networks (WSN)** — Understanding device registration, data collection, and real-time control in IoT environments

---

## Author

**Divyanshu Kumar**  
B.Tech Electronics & Communication Engineering

[![GitHub](https://img.shields.io/badge/GitHub-Profile-181717?style=flat-square&logo=github)](https://github.com/Divyanshukumar2005)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=flat-square&logo=linkedin)](https://linkedin.com/in/YOUR_LINKEDIN)

---

*Built with Cisco Packet Tracer 8.2.2 as part of B.Tech ECE curriculum.*
