# Network Topology

---

# Objective

This document describes the network architecture, addressing scheme, interface configuration, and traffic flow used throughout the pfSense firewall home lab.

The topology was intentionally designed to simulate a small enterprise network where all outbound traffic is inspected and routed through a dedicated firewall before reaching external networks.

---

# Network Architecture

![Network Topology](../diagrams/network-topology.png)

The lab consists of four primary components:

1. Internet
2. VirtualBox NAT Router
3. pfSense Community Edition Firewall
4. Ubuntu Server

The firewall separates the trusted internal LAN from the untrusted external network while performing routing, firewall inspection, DHCP, DNS forwarding, and Network Address Translation (NAT).

---

# Logical Network Design

The environment is divided into two Layer 3 networks.

| Network | Address Space | Purpose |
|----------|---------------|---------|
| WAN | 10.0.2.0/24 | External Network |
| LAN | 192.168.10.0/24 | Internal Trusted Network |

Traffic between these networks is controlled by pfSense.

---

# IP Addressing Plan

| Device | Interface | IP Address |
|---------|-----------|------------|
| VirtualBox NAT Router | Gateway | 10.0.2.2 |
| pfSense | WAN (em0) | 10.0.2.15 |
| pfSense | LAN (em1) | 192.168.10.1 |
| Ubuntu Server | Ethernet | 192.168.10.100 |

---

# Interface Configuration

## WAN Interface

- Interface: em0
- Address: 10.0.2.15/24
- Gateway: 10.0.2.2

The WAN interface connects pfSense to the VirtualBox NAT router, providing Internet connectivity for the lab.

---

## LAN Interface

- Interface: em1
- Address: 192.168.10.1/24

The LAN interface serves as the default gateway for internal systems and provides DHCP and DNS forwarding services.

---

# Traffic Flow

Outbound traffic follows this sequence:

```text
Ubuntu Server
        │
        ▼
LAN Interface
        │
Firewall Rule Evaluation
        │
State Table
        │
Source NAT (PAT)
        │
WAN Interface
        │
VirtualBox NAT Router
        │
Internet
```

Return traffic is automatically permitted because pfSense is a stateful firewall. Replies to established outbound connections are matched against the firewall's state table and forwarded back to the originating host without requiring an additional inbound firewall rule.

---

# Design Decisions

Several implementation decisions were made during the design of this lab.

### Why pfSense?

pfSense is a widely used open-source firewall platform that provides enterprise-grade firewall functionality, routing, NAT, VPN support, diagnostics, and logging.

---

### Why VirtualBox NAT?

VirtualBox NAT provides Internet connectivity without requiring changes to the physical home network, making it suitable for isolated testing environments.

---

### Why Ubuntu Server?

Ubuntu Server provides a lightweight Linux system for generating and analyzing network traffic while consuming minimal resources.

---

### Why Separate LAN and WAN Networks?

Separating trusted and untrusted networks allows firewall policies, routing decisions, and NAT behavior to be observed and verified in a controlled environment.

---

# Verification

The topology was validated using multiple diagnostic methods:

- Ping
- Traceroute
- DNS Lookup
- Packet Capture
- Firewall Logs
- ARP Table
- Routing Table
- State Table

These verification steps confirmed that routing, firewall rules, and NAT operated as expected.

---

# Key Takeaways

This topology demonstrates the core components of a firewall deployment:

- Network segmentation
- Stateful packet filtering
- Source NAT (PAT)
- DHCP and DNS services
- Routing between trusted and untrusted networks
- Verification using packet analysis and diagnostic tools

This architecture serves as the foundation for future projects involving VLAN segmentation, Active Directory, SIEM integration, and detection engineering.