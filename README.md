# 🌐 Multi-Campus University Network Design

[![Cisco Packet Tracer](https://img.shields.io/badge/Cisco-Packet%20Tracer-1BA0D7?logo=cisco)](https://www.netacad.com/courses/packet-tracer)
[![Network Design](https://img.shields.io/badge/Network-Enterprise%20Design-blue)](https://github.com)
[![OSPF](https://img.shields.io/badge/Protocol-OSPF-orange)](https://en.wikipedia.org/wiki/Open_Shortest_Path_First)
[![EIGRP](https://img.shields.io/badge/Protocol-EIGRP-red)](https://en.wikipedia.org/wiki/Enhanced_Interior_Gateway_Routing_Protocol)
[![License](https://img.shields.io/badge/License-Educational-green.svg)](LICENSE)

A comprehensive enterprise-level network infrastructure design for a multi-campus university environment, featuring **six interconnected campuses** with centralized management, high availability, and robust security. This project implements a complete network design consisting of six campuses interconnected through a central core network, providing secure, scalable, and high-performance connectivity supporting thousands of students, staff, servers, and wireless users.

---

## 📋 Table of Contents

- [Project Overview](#-project-overview)
- [Network Architecture](#-network-architecture)
- [VLAN Structure](#-vlan-structure)
- [Wireless Network Design](#-wireless-network-design)
- [Security Measures](#-security-measures)
- [IP Addressing Plan](#-ip-addressing-plan)
- [Design Benefits](#-design-benefits)
- [Getting Started](#-getting-started)
- [Packet Tracer Simulation](#-packet-tracer-simulation)
- [Technologies Used](#-technologies-used)
- [Authors](#-authors)

---

## 🎯 Project Overview

### Key Features

- ✨ **Scalable Architecture** - Built on 10.0.0.0/8 private IP block with /16 allocation per campus
- 🔄 **Dual Routing Protocols** - OSPF Multi-Area for intra-campus and EIGRP for inter-campus routing
- 📡 **Centralized Wireless Management** - Wireless LAN Controller (WLC) with Lightweight Access Points
- 🔐 **VLAN Segmentation** - Secure departmental isolation across all campuses
- ⚡ **High Availability** - Redundant links, dual routers, and loop-free Layer-2 design
- 🛡️ **Enterprise Security** - ACLs, WPA2 Enterprise, routing protocol authentication, and VLAN segmentation

---

## 🏗️ Network Architecture

### Campus Infrastructure

The network consists of six campuses (A through F) with **Campus A** serving as the central hub:

```
┌─────────────────────────────────────────────────┐
│            Campus A (Core Hub)                  │
│  • Core Router + OSPF Area 0                    │
│  • Centralized DHCP Services                    │
│  • Wireless LAN Controller (WLC)                │
└──────────┬──────────┬──────────┬────────────────┘
           │          │          │
    ┌──────┴───┐  ┌──┴──────┐  ├─────────┐
    │          │  │         │  │         │
┌───▼───┐  ┌──▼───┐  ┌──▼───┐  ┌──▼───┐  ┌──▼───┐
│Campus │  │Campus│  │Campus│  │Campus│  │Campus│
│   B   │  │  C   │  │  D   │  │  E   │  │  F   │
└───────┘  └──────┘  └──────┘  └──────┘  └──────┘
```

**Campus Roles:**
- 🏢 **Campus A** - Core Router + Centralized Services (DHCP, WLC)
- 🏫 **Campuses B-F** - Branch campuses connected to Campus A via dedicated WAN links

---

### Routing Design

#### 🔵 Interior Routing (OSPF Multi-Area)

- Each campus runs OSPF internally
- **Area 0** operates on the Core Router at Campus A
- Campus routers connect to Area 0 using point-to-point WAN links
- Ensures fast convergence and efficient routing within campuses

#### 🔴 Exterior Routing (EIGRP)

- **Autonomous System Number:** AS 100
- Handles route exchange between campuses
- Load balancing across inter-campus links
- Redistribution between OSPF and EIGRP at Campus A Core Router

---

### WAN Design

Point-to-point connections using **/30 subnets** from `10.255.x.x/30`:

| Connection | Subnet | Router A IP | Router B IP |
|------------|--------|-------------|-------------|
| Campus A ↔ Campus B | `10.255.1.0/30` | 10.255.1.1 | 10.255.1.2 |
| Campus A ↔ Campus C | `10.255.2.0/30` | 10.255.2.1 | 10.255.2.2 |
| Campus A ↔ Campus D | `10.255.3.0/30` | 10.255.3.1 | 10.255.3.2 |
| Campus A ↔ Campus E | `10.255.4.0/30` | 10.255.4.1 | 10.255.4.2 |
| Campus A ↔ Campus F | `10.255.5.0/30` | 10.255.5.1 | 10.255.5.2 |

---

## 📊 VLAN Structure

Common VLANs deployed across **all campuses**:

| VLAN ID | Department | Purpose | Subnet Example |
|---------|------------|---------|----------------|
| **VLAN 10** | Admin | Administrative staff | 10.X.10.0/24 |
| **VLAN 20** | Student | Student network | 10.X.20.0/24 |
| **VLAN 30** | Faculty | Faculty members | 10.X.30.0/24 |
| **VLAN 40** | Servers | Campus servers | 10.X.40.0/24 |
| **VLAN 50** | Wireless | Wireless users | 10.X.50.0/24 |
| **VLAN 60** | Guest WiFi | Guest network access | 10.X.60.0/24 |

> **Note:** X represents the campus number (1-6)

---

## 📡 Wireless Network Design

### WLC Deployment

- 📍 **Location:** Campus A VLAN 50
- 🎛️ **Management:** Centralized control of all APs across six campuses
- 📶 **AP Mode:** Lightweight (CAPWAP protocol)

### SSID Configuration

| SSID Type | Authentication | Access Level |
|-----------|----------------|--------------|
| 🔐 **Staff/Student SSID** | WPA2 Enterprise | Full network access |
| 🌐 **Guest SSID** | Limited access | Bandwidth controls |

---

## 🔒 Security Measures

Our network implements a **multi-layered security approach**:

| Security Layer | Implementation |
|----------------|----------------|
| 🛡️ **Access Control Lists (ACLs)** | Traffic filtering and policy enforcement |
| 🔐 **WPA2 Enterprise** | Secure wireless authentication |
| 🔑 **Routing Protocol Authentication** | OSPF and EIGRP MD5 authentication |
| 🏢 **VLAN Segmentation** | Network isolation by department |
| 🔌 **Port Security** | MAC address binding on access switches |

---

## 🖥️ DHCP Design

**Centralized DHCP servers** located in Campus A provide IP addresses for:

- ✅ Admin department
- ✅ Student network
- ✅ Faculty network
- ✅ Server infrastructure
- ✅ Wireless clients
- ✅ Guest WiFi users

**Configuration:** Router-on-a-Stick with `ip helper-address` forwards DHCP requests from remote campuses.

---

## 📋 IP Addressing Plan

### Primary IP Block

```
10.0.0.0/8
```

### Per-Campus Allocation

Each campus receives a **/16 subnet**, supporting up to **65,536 IP addresses**:

| Campus | IP Range | Available Hosts |
|--------|----------|-----------------|
| 🏢 **Campus A** | `10.1.0.0/16` | 65,534 |
| 🏫 **Campus B** | `10.2.0.0/16` | 65,534 |
| 🏫 **Campus C** | `10.3.0.0/16` | 65,534 |
| 🏫 **Campus D** | `10.4.0.0/16` | 65,534 |
| 🏫 **Campus E** | `10.5.0.0/16` | 65,534 |
| 🏫 **Campus F** | `10.6.0.0/16` | 65,534 |

---

## 🎯 Design Benefits

| Benefit | Description |
|---------|-------------|
| ✅ **Scalable** | 10.0.0.0/8 with /16 per campus supports significant population growth |
| ✅ **Fast Convergence** | OSPF Multi-Area ensures efficient routing within campuses |
| ✅ **Robust Connectivity** | EIGRP provides high performance and load balancing between campuses |
| ✅ **Centralized Management** | WLC in Campus A reduces operational overhead |
| ✅ **High Security** | Multi-layered security approach with ACLs, encryption, and segmentation |
| ✅ **Easy Administration** | Campus A hosts all critical services for simplified management |

---

## 🛠️ Technologies Used

### Routing & Switching
- 🔄 **OSPF** (Multi-Area) - Interior Gateway Protocol
- 🔄 **EIGRP** (AS 100) - Enhanced Interior Gateway Routing Protocol
- 🔀 **VLANs** - Virtual LAN Segmentation
- 🌳 **STP** - Spanning Tree Protocol
- 🔗 **VLAN Trunking** - Inter-switch communication

### Wireless & Services
- 📡 **Centralized WLC** - Wireless LAN Controller with CAPWAP
- 🖥️ **DHCP** - Dynamic Host Configuration Protocol
- 🌐 **DNS** - Domain Name System

### Security
- 🛡️ **ACLs** - Access Control Lists
- 🔐 **WPA2 Enterprise** - Wireless Security
- 🔑 **MD5 Authentication** - Routing Protocol Security

---

## 📁 Repository Structure

```
multi-campus-network-design/
├── 📄 CN_Course_Project.docx    # Complete project documentation
├── 🌐 CN_Course_Project.pkt     # Cisco Packet Tracer simulation file
└── 📖 README.md                  # This file
```

---

## 💻 Packet Tracer Simulation

This repository includes a fully functional **Cisco Packet Tracer simulation file**: `CN_Course_Project.pkt`

### Opening the Simulation

1. Download and install [Cisco Packet Tracer](https://www.netacad.com/courses/packet-tracer) (version 8.0 or higher recommended)
2. Download the `CN_Course_Project.pkt` file from this repository
3. Open the file in Cisco Packet Tracer
4. Explore the network topology and device configurations

### What's Included in the Simulation

- ✅ All six campus networks (A through F)
- ✅ Configured routers with OSPF and EIGRP
- ✅ Layer-2 switches with VLAN configurations
- ✅ Wireless LAN Controller (WLC) and Access Points
- ✅ DHCP servers
- ✅ End devices (PCs, laptops, servers)
- ✅ WAN interconnections between campuses

### Testing the Network

You can test various scenarios in the simulation:

| Test Type | Command/Action |
|-----------|----------------|
| 🔌 **Connectivity Testing** | Use `ping` and `traceroute` between different campuses and VLANs |
| 🖥️ **DHCP Testing** | Check if devices receive IP addresses automatically |
| 🗺️ **Routing Protocol Verification** | View OSPF and EIGRP routing tables (`show ip route`) |
| 📡 **Wireless Connectivity** | Test wireless client connections |
| ⚡ **Failover Testing** | Disable links to test redundancy and convergence |

---

## 🚀 Getting Started

### Prerequisites

- ✅ **Cisco Packet Tracer** (version 8.0 or higher) - [Download here](https://www.netacad.com/courses/packet-tracer)
- ✅ Basic understanding of networking concepts (TCP/IP, routing, switching)
- ✅ Familiarity with Cisco IOS commands
- ✅ Knowledge of VLAN, OSPF, and EIGRP concepts

### Quick Start

1. **Clone the repository**

   ```bash
   git clone https://github.com/ayesha189/multi-campus-network-design.git
   cd multi-campus-network-design
   ```

2. **Open the simulation**

   - Launch Cisco Packet Tracer
   - Open `CN_Course_Project.pkt`
   - The complete network topology will load with all configurations

3. **Explore the network**

   - Click on devices to view configurations
   - Use simulation mode to visualize packet flow
   - Test connectivity between different campuses and VLANs

### Building From Scratch (Optional)

If you want to recreate the network from scratch for learning purposes:

1. ✅ Set up the physical or virtual network topology
2. ✅ Configure IP addressing according to the addressing plan
3. ✅ Implement VLAN structure on all switches
4. ✅ Configure OSPF within each campus
5. ✅ Set up EIGRP between campus routers
6. ✅ Deploy and configure WLC for wireless management
7. ✅ Configure DHCP services
8. ✅ Implement security policies (ACLs, authentication)
9. ✅ Test connectivity and failover scenarios

> **💡 Tip:** Reference the provided `.pkt` file for complete device configurations!

---

## 📖 Documentation

The complete network design documentation includes:

- 📊 Detailed topology diagrams
- ⌨️ CLI configurations for all devices
- 🔒 Security policies
- 🔀 VLAN configurations
- 🗺️ Routing protocol setup
- 📡 Wireless controller configuration

📄 **See full documentation:** `CN_Course_Project.docx`

---

## 📝 Academic Details

- **Course:** Computer Networks
- **Project Type:** Final Project
- **Institution:** Educational University Project

---

## 👥 Authors

**Team Members:**

- **Ayesha Rauf** (23f-0807) — [@ayesha189](https://github.com/ayesha189)
- **Nimra Shahid** (23f-0734) — [@NIMRAH-S](https://github.com/NIMRAH-S)
- **Aqsa Ishaq** (23f-0839) — [@aqsaishaq573-aqi](https://github.com/aqsaishaq573-aqi)

---

## 🙏 Acknowledgments

- Computer Networks Course Project
- Cisco Networking Academy
- University Faculty and Peers

---

## 📄 License

This project is created for **educational purposes** as part of a university course assignment.

---

## ⭐ Support

If you found this project helpful or educational, please consider giving it a star!

---

<div align="center">

### 🌐 Happy Networking! 🚀

Made with ❤️ for learning enterprise network design

</div>
