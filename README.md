# 🌐 IoT Smart Home Sensor Network — Cisco Packet Tracer

> Designed, implemented, and evaluated a complete IoT-based smart home network with automated control logic and network performance analysis using Cisco Packet Tracer 8.2.2

---

## 📋 Overview

This project simulates a smart home IoT network where multiple sensors and actuators communicate through a wireless router and IoT server. Automation rules enable intelligent control based on real-time sensor inputs. Network performance was quantitatively analyzed using PDR, Throughput, and End-to-End Delay metrics.

---

## 🛠️ Tools & Technologies

| Category | Details |
|---|---|
| **Simulation Tool** | Cisco Packet Tracer 8.2.2 |
| **Network Hardware** | WRT300N Wireless Router, Cisco 2960-24TT Switch |
| **IoT Server** | Packet Tracer IoT Server (Registration + Automation) |
| **Wireless Security** | WPA2-PSK / AES |
| **Protocol** | Wi-Fi (802.11), DHCP, ICMP |

---

## 🔌 IoT Devices Used

| Device | Role |
|---|---|
| Motion Sensor | Detects human presence |
| Door Sensor | Tracks door lock/unlock state |
| Temperature Sensor | Monitors ambient temperature |
| Smoke Detector | Fire hazard detection |
| Smart Light | Automated lighting control |
| Smart Fan | Variable speed fan actuator |
| Security Camera | Visual monitoring (Webcam) |

---

## 🏗️ Network Architecture

```
[IoT Server] ──┐
[PC]           ├── [2960-24TT Switch] ── [WRT300N Wireless Router]
               │                                │
               │              ┌─────────────────┼──────────────────┐
               │         [Motion Sensor]  [Door Sensor]  [Temp Sensor]
               │         [Smoke Detector] [Smart Light]  [Smart Fan]
               │         [Security Cam]   [Smartphone x2]
```

- **Topology:** Star (Switch as central hub)
- **IoT Server IP (Static):** `192.168.0.10`
- **DHCP Range:** `192.168.0.100 – 192.168.0.149`
- **Router Gateway:** `192.168.0.1`
- **SSID:** `IoT_Wireless`

---

## ⚙️ Automation Rules Configured

| Rule Name | Condition | Action |
|---|---|---|
| Door_Open_Light_Fan_ON | Door Sensor → Unlock | Light ON + Fan HIGH |
| Door_Close_Light_Fan_OFF | Door Sensor → Lock | Light OFF + Fan OFF |
| Motion_Detected_Light_ON | Motion Sensor → True | Light ON |
| No_Motion_Light_OFF | Motion Sensor → False | Light OFF |
| High_Temperature_Fan_ON | Temp > 25.0 °C | Fan HIGH |
| Normal_Temperature_Fan_OFF | Temp < 25.0 °C | Fan LOW |

---

## 📊 Network Performance Results

### Packet Delivery Ratio (PDR)

```
Packets Sent     : 100
Packets Received : 100
Packets Lost     : 0

PDR = (100 / 100) × 100 = 100%
```

✅ **Zero packet loss — excellent network reliability**

---

### Throughput Calculation

```
Packet Size     : 32 bytes
Total Packets   : 100
Total Data      : 3200 bytes = 25,600 bits
Time Elapsed    : ~4.1 seconds

Throughput = 25,600 / 4.1 ≈ 6,243.9 bps ≈ 6.24 kbps
```

> Note: This measures ICMP test traffic throughput. The WRT300N supports up to 54 Mbps (802.11g) theoretical capacity.

---

### End-to-End Delay

```
Average RTT    : 41 ms
Min RTT        : 11 ms
Max RTT        : 159 ms

One-Way Delay  = RTT / 2 = 41 / 2 = 20.5 ms
```

✅ **20.5 ms average delay — well within 100–500 ms acceptable range for smart home IoT**

---

## 📁 Repository Structure

```
iot-sensor-network-packet-tracer/
│
├── README.md                         ← This file
├── IoT_SmartHome.pkt                 ← Cisco Packet Tracer simulation file
├── docs/
│   ├── network_topology.png          ← Network diagram screenshot
│   ├── automation_rules.png          ← IoT Server conditions screenshot
│   └── ping_results.png              ← PDR test output
└── report/
    └── Experiment2_FullReport.pdf    ← Detailed lab report
```

---

## 🚀 How to Run

1. **Install** Cisco Packet Tracer (v8.0 or above): [Download here](https://www.netacad.com/cisco-packet-tracer)
2. **Open** `IoT_SmartHome.pkt` in Packet Tracer
3. **Wait** ~30 seconds for all devices to associate with the wireless router
4. **Open** PC → Desktop → IoT Monitor → Login with `admin / admin`
5. **Test automation:** Click on Door Sensor → toggle Lock/Unlock → observe Light and Fan response
6. **Run PDR test:** PC → Desktop → Command Prompt → `ping 192.168.0.115 -n 100`

---

## 📈 Key Learnings

- IoT architecture: sensor → server → actuator pipeline
- DHCP-based auto-configuration for large device networks
- WPA2-PSK wireless security implementation
- Automation rule engine logic on IoT Server
- Quantitative network analysis: PDR, Throughput, E2E Delay

---

## 👤 Author

**Divyanshu Kumar**  
B.Tech ECE, University of Delhi (2023–2027)  
[LinkedIn](https://www.linkedin.com/in/divyanshu-kumar-7625a8315) | [GitHub](https://github.com/Divyanshukumar2005)

---

## 📄 License

MIT License — feel free to use for educational purposes.
