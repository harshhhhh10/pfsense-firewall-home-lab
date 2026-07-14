# Environment Deployment

---

# Objective

This document describes the deployment of the pfSense firewall home lab, including the virtualization platform, virtual machine configuration, operating systems, and network adapter assignments.

The objective was to build an isolated and repeatable environment that closely resembles a small enterprise network while remaining safe to run on a personal computer.

---

# Deployment Overview

The lab was deployed using Oracle VirtualBox.

The environment consists of two virtual machines:

- pfSense Community Edition
- Ubuntu Server

The firewall acts as the gateway between the trusted internal LAN and the external network provided by VirtualBox NAT.

---

# Lab Components

| Component | Version / Purpose |
|------------|------------------|
| Hypervisor | Oracle VirtualBox |
| Firewall | pfSense Community Edition |
| Client | Ubuntu Server |
| Host Operating System | Windows |
| Internet Access | VirtualBox NAT |

---

# Virtual Machine Configuration

## pfSense

| Resource | Configuration |
|----------|---------------|
| CPUs | 2 |
| Memory | 2 GB *(adjust to your actual value)* |
| Disk | 20 GB *(adjust if different)* |
| Network Adapter 1 | NAT |
| Network Adapter 2 | Internal Network |

---

## Ubuntu Server

| Resource | Configuration |
|----------|---------------|
| CPUs | 2 |
| Memory | 2 GB *(adjust to your actual value)* |
| Disk | 25 GB *(adjust if different)* |
| Network Adapter | Internal Network |

---

# Network Adapter Assignment

## pfSense

| Adapter | Connected To | Purpose |
|----------|--------------|----------|
| Adapter 1 | NAT | WAN |
| Adapter 2 | Internal Network | LAN |

---

## Ubuntu Server

| Adapter | Connected To |
|----------|--------------|
| Adapter 1 | Internal Network |

This configuration ensures that all outbound traffic from Ubuntu is routed through the pfSense firewall before reaching the Internet.

---

# Initial Configuration

After installation, the following configuration tasks were completed:

- Assigned WAN and LAN interfaces
- Configured LAN IP address
- Configured DHCP
- Configured DNS Forwarder
- Verified Internet connectivity
- Verified routing
- Verified firewall operation

---

# Design Decisions

### Why VirtualBox?

Oracle VirtualBox is free, cross-platform, and supports multiple isolated virtual networks, making it suitable for building repeatable cybersecurity labs.

---

### Why Two Network Adapters for pfSense?

A firewall requires at least two interfaces:

- WAN
- LAN

This allows pfSense to inspect and route traffic between trusted and untrusted networks.

---

### Why Internal Network?

Using an isolated Internal Network prevents lab traffic from directly reaching the physical home network while allowing pfSense to control all communication.

---

# Verification

The deployment was validated by confirming:

- Both virtual machines booted successfully.
- pfSense detected both interfaces.
- Ubuntu received the expected IP address.
- Internet connectivity was available through pfSense.
- DNS resolution functioned correctly.
- Firewall logs showed outbound connections.

---

# Screenshots

Include:

- VirtualBox VM settings (pfSense)
- VirtualBox VM settings (Ubuntu)
- pfSense console after installation
- Interface assignment screen

---

# Key Takeaways

The deployment phase established a repeatable virtual networking environment that serves as the foundation for all subsequent firewall configuration, packet analysis, and troubleshooting activities.