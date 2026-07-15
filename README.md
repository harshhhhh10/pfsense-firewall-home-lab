# 🛡️ Enterprise Firewall & Network Security Home Lab using pfSense

<p align="center">
  <img src="https://img.shields.io/badge/Platform-VirtualBox-blue" alt="Platform">
  <img src="https://img.shields.io/badge/Firewall-pfSense-orange" alt="Firewall">
  <img src="https://img.shields.io/badge/OS-Ubuntu_Server-E95420" alt="OS">
  <img src="https://img.shields.io/badge/License-MIT-green" alt="License">
  <img src="https://img.shields.io/badge/Project-Completed-success" alt="Status">
</p>

> A production-inspired firewall and network security laboratory built using **pfSense Community Edition** to demonstrate enterprise firewall administration, Network Address Translation (NAT), routing, packet analysis, stateful inspection, and troubleshooting in a virtual environment.

---

## 📖 Table of Contents

* [Project Overview](#-project-overview)
* [Project Objectives](#-project-objectives)
* [Technologies Used](#-technologies)
* [Architecture](#-architecture)
* [Features Implemented](#-features-implemented)
* [Documentation](#-documentation)
* [Project Gallery](#-project-gallery)
* [Skills Demonstrated](#-skills-demonstrated)
* [Future Improvements](#-future-improvements)
* [References](#-references)
* [Author](#-author)

---

## 📌 Project Overview

This project demonstrates the deployment, configuration, verification, and troubleshooting of a pfSense firewall within a virtualized home lab environment. 

The lab was built to simulate fundamental enterprise networking concepts including firewall policy management, dynamic routing, Network Address Translation (NAT), packet inspection, and stateful tracking pipelines. 

Rather than simply applying static configuration toggles, this project focuses heavily on empirical verification—analyzing exactly how packet frames change state and transform as they traverse distinct security layers.

---

## 🎯 Project Objectives

* Deploy pfSense in an isolated, multi-interface hypervisor environment.
* Configure functional WAN, LAN, and administrative interface endpoints.
* Manage dynamic endpoint initialization via centralized DHCP and secure DNS Unbound engines.
* Code and enforce strict stateful firewall rules matching least-privilege standards.
* Implement custom Hybrid Outbound NAT and Port Forwarding (Destination NAT) rules.
* Capture and analyze raw network traffic frames across interface boundaries.
* Map and validate localized address resolution behaviors using diagnostic utilities.
* Document systemic baseline performance and incident troubleshooting frameworks.

---

## 🛠 Technologies

| Core Component | Implementation Role / Purpose |
| :--- | :--- |
| **pfSense CE** | Edge Security Gateway, Router, and Packet Filtering Engine |
| **Oracle VirtualBox** | Type-2 Hypervisor Platform for isolated virtualization |
| **Ubuntu Desktop** | Internal Endpoint Client node for system validation testing |
| **Python HTTP Server** | Local daemon testing asset to verify inbound redirection loops |
| **ICMP / UDP / TCP** | Structural protocol tracking targets used across packet analysis phases |

---

## 🏗 Architecture

<p align="center">
  <img src="diagrams/pfsense-virtualbox-lab-topology.png" alt="Network Topology">
</p>

The architecture creates an enterprise-styled DMZ demarcation pattern inside the host sandbox system:
* **VirtualBox NAT Network Backplane:** Maps out the simulated public provider perimeter.
* **The pfSense Security Node:** Bridges unauthenticated assets to internal infrastructure zones.
* **WAN Segment (`10.0.2.0/24`):** External entry domain relying on default gateway routing tracking.
* **LAN Subnet (`192.168.10.0/24`):** High-trust domain hosting primary system workloads.

---

## ✨ Features Implemented

* **Interface Provisioning:** Hardened driver binding and layer-3 subnet segmentation configurations.
* **Stateful Access Control Policies:** Granular time-based restrictions and strict alias-driven block rules.
* **Dynamic Scoping Daemons:** Active local DHCP allocation pools paired with responsive DNS record tracking.
* **Hybrid Outbound NAT Mappings:** Controlled source header translation schema for outbound privacy.
* **Inbound Destination Port Forwarding:** Encapsulated mapping of external port requests down to target hosts.
* **Concurrent Interface Wire Diagnostics:** Deep frame verification loops capturing before-and-after NAT snapshots.

---

## 📚 Documentation

| Module ID | Documentation Title | Repository Navigation |
| :--- | :--- | :--- |
| **01** | Project Overview | [View Document](docs/01-project-overview.md) |
| **02** | Network Topology | [View Document](docs/02-network-topology.md) |
| **03** | Environment Deployment | [View Document](docs/03-environment-deployment.md) |
| **04** | Network Configuration | [View Document](docs/04-network-configuration.md) |
| **05** | Firewall Rules Enforcement | [View Document](docs/05-firewall-rules.md) |
| **06** | Network Address Translation (NAT) | [View Document](docs/06-nat.md) |
| **07** | Packet Analysis and Captures | [View Document](docs/07-packet-analysis.md) |
| **08** | Network Diagnostics and Tables | [View Document](docs/08-network-diagnostics.md) |
| **09** | Troubleshooting Frameworks | [View Document](docs/09-troubleshooting.md) |
| **10** | Lessons Learned & Technical Review | [View Document](docs/10-lessons-learned.md) |

---

## 📸 Project Gallery

The active artifacts verifying this topology are systematically cross-referenced within the sub-documentation files:
* Core pfSense Resource and Monitoring System Dashboards
* WAN Interconnect and LAN Gateway Port Maps
* Layer 4 Stateful Rules Policy Inventories
* Hybrid NAT Mapping Blocks & Port Redirection Tables
* Dual-Interface Packet Capture Verification Streams
* Filter Logs showing dropped ICMP, TCP, and UDP sessions

---

## 🧪 Skills Demonstrated

### Core Infrastructure & Routing
* Structured subnet masking planning using modern CIDR formatting guidelines.
* Stateful boundary routing across multi-zone routing engines.
* Centralized infrastructure configuration optimization spanning DHCP and Unbound caching architectures.

### Network Defense Engineering
* Application of Least Privilege principles across layer-3 access control lists.
* Deployment and tuning of translation configurations (SNAT, PAT, DNAT).
* Interpretation of live state table flag states (`ESTABLISHED:ESTABLISHED`) to trace handshake life cycles.

### Security Analytics & Telemetry
* Wire monitoring using pcap parsing filters to capture and review raw frame headers.
* Reading firewall tracking entries to verify rule IDs and find blocked network traffic patterns.
* System troubleshooting using deep interface ping routines, route tracing, and active log mining.

---

## 🚀 Future Improvements

This pfSense firewall installation forms the structural core network routing and security foundation for a scaling enterprise security home lab. Future lab expansions will build upon this layout using the following roadmaps:

1. **Enterprise VLAN Segmentation:** Add explicit `OPT` virtual interfaces on the pfSense firewall using 802.1Q tags to isolate Active Directory, SIEM, and workstation traffic into distinct broadcast domains.
2. **Active Directory Lab Deployment:** Stand up a Windows Server domain controller cluster behind the LAN gateway to manage centralized domain authentication and enforce baseline security Group Policy Objects (GPOs).
3. **Windows Event Forwarding (WEF) Setup:** Configure group policy subscriptions to automatically pull system, security, and application logs from domain workstations down to a centralized log-collector endpoint.
4. **Sysmon Deployment & Tuning:** Roll out the Microsoft System Monitor (Sysmon) extension across endpoints to collect advanced telemetry, including process creations, network socket origins, and raw memory loading hooks.
5. **Wazuh SIEM Integration:** Deploy a central Wazuh manager node in a dedicated management subnet to ingest endpoint logs and systematically parse data against active threat intelligence metrics.
6. **Detection Engineering Practice:** Author custom Sigma rule sets and SIEM alert logic designed to catch suspicious actions, such as lateral movement attempts or unauthorized external DNS tunneling.
7. **Incident Response & Threat Hunting:** Execute controlled malware simulations within isolated subnets to practice analyzing memory structure artifacts, tracking process execution paths, and conducting live post-breach forensics.

---

## 📖 References

* **Netgate pfSense Technical Documentation:** [Core Reference Guide](https://netgate.com)
* **RFC 791:** Internet Protocol (IPv4 Core Routing Standards)
* **RFC 1918:** Address Allocation for Private Internets (Subnet Boundaries)
* **RFC 4787:** Network Address Translation (NAT) Behavioral Requirements for Unicast UDP

---

## 👨‍💻 Author

**Harsh Soni**  
[GitHub Profile](https://github.com)  
*Cybersecurity Engineer | Defensive Security Practitioner | Threat Hunting Enthusiast*
