# 🛡️ Enterprise Firewall & Network Security Home Lab using pfSense

<p align="center">

![Platform](https://img.shields.io/badge/Platform-VirtualBox-blue)
![Firewall](https://img.shields.io/badge/Firewall-pfSense-orange)
![Operating System](https://img.shields.io/badge/OS-Ubuntu_Server-E95420)
![License](https://img.shields.io/badge/License-MIT-green)
![Status](https://img.shields.io/badge/Project-Completed-success)

</p>

> A production-inspired firewall and network security laboratory built using **pfSense Community Edition** to demonstrate enterprise firewall administration, Network Address Translation (NAT), routing, packet analysis, stateful inspection, and troubleshooting in a virtual environment.

---

## 📖 Table of Contents

- [Project Overview](#-project-overview)
- [Objectives](#-project-objectives)
- [Technologies Used](#-technologies)
- [Architecture](#-architecture)
- [Features Implemented](#-features-implemented)
- [Documentation](#-documentation)
- [Project Gallery](#-project-gallery)
- [Skills Demonstrated](#-skills-demonstrated)
- [Future Improvements](#-future-improvements)
- [References](#-references)

---

## 📌 Project Overview

This project demonstrates the deployment, configuration, verification, and troubleshooting of a pfSense firewall within a virtual home lab environment.

The lab was built to simulate fundamental enterprise networking concepts including firewall policy management, routing, Network Address Translation (NAT), packet analysis, and stateful packet filtering.

Rather than only configuring the firewall, the project focuses on understanding how traffic flows through the network and how pfSense processes packets at each stage.

---

## 🎯 Project Objectives

- Deploy pfSense in a virtualized environment
- Configure WAN and LAN interfaces
- Configure DHCP and DNS services
- Implement firewall rules
- Configure Source NAT and Port Forwarding
- Capture and analyze network traffic
- Investigate routing and ARP behavior
- Understand Stateful Packet Inspection (SPI)
- Perform network troubleshooting using pfSense diagnostic tools
- Document the complete implementation

---

## 🛠 Technologies

| Technology | Purpose |
|------------|---------|
| pfSense CE | Firewall & Router |
| Oracle VirtualBox | Virtualization Platform |
| Ubuntu Desktop | Internal Client |
| Python HTTP Server | Web Server Testing |
| ICMP | Connectivity Testing |
| DNS | Name Resolution |
| TCP/IP | Network Communication |

---

## 🏗 Architecture



<p align="center">

![Network Topology](diagrams/pfsense-virtualbox-lab-topology.png)

</p>

The lab consists of:

- VirtualBox NAT Network
- pfSense Firewall
- Ubuntu Desktop
- Internal LAN (192.168.10.0/24)
- WAN Network (10.0.2.0/24)

---

## ✨ Features Implemented

- Interface Configuration
- Firewall Rules
- DHCP Configuration
- DNS Resolution
- Source NAT
- Destination NAT (Port Forward)
- Packet Capture
- Firewall Logging
- Routing Analysis
- ARP Analysis
- Stateful Packet Inspection
- Backup & Restore
- CLI Troubleshooting

---

## 📚 Documentation

| Document | Description |
|----------|-------------|
| 01 | Project Overview | [View](docs/01-project-overview.md) | 
| 02 | Network Topology | [View](docs/02-network-topology.md) |
| 03 | Installation | [View](docs/03-environment-deployment.md) |
| 04 | Network Configuration | [View](docs/04-network-configuration.md) |
| 05 | Firewall Rules | [View](docs/05-firewall-rules.md) |
| 06 | Network Address Translation | [View](docs/06-nat.md) |
| 07 | Packet Analysis | [View](docs/07-packet-analysis.md) |
| 08 | Network Diagnostics | [View](docs/08-network-diagnostics.md) |
| 09 | Troubleshooting | [View](docs/09-troubleshooting.md) |
| 10 | Lessons Learned | [View](docs/10-lessons-learned.md) |

---

## 📸 Screenshots

## 📸 Project Gallery

The following screenshots are documented throughout the project:

- pfSense Dashboard
- WAN & LAN Interface Configuration
- Firewall Rules
- Outbound NAT Configuration
- Packet Capture Analysis
- Firewall Logs
- DNS Lookup
- ARP Table
- Routing Table
- State Table
- Backup & Restore

---

## 🧪 Skills Demonstrated

### Networking

- IPv4 Addressing
- Routing
- Default Gateway
- DNS
- ARP
- ICMP

### Firewall Administration

- Stateful Packet Inspection (SPI)
- Firewall Rule Management
- NAT Configuration
- Port Forwarding
- Logging
- Diagnostics

### Network Analysis

- Packet Capture
- Firewall Log Analysis
- Route Verification
- State Table Analysis
- Troubleshooting

---

## 🚀 Future Improvements

This project is the foundation of a larger enterprise cybersecurity home lab.

Planned future projects include:

1. Enterprise VLAN Segmentation
2. Active Directory Lab
3. Windows Event Forwarding
4. Sysmon Deployment
5. Wazuh SIEM Integration
6. Detection Engineering
7. Incident Response & Threat Hunting

---

## 📖 References

- pfSense Documentation
- RFC 791 – Internet Protocol (IPv4)
- RFC 826 – Address Resolution Protocol (ARP)
- RFC 1035 – Domain Name System (DNS)

---

## 👨‍💻 Author

**Harsh Soni**

Cybersecurity | Defensive Security | SOC Analyst Journey
