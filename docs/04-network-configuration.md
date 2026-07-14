# Network Configuration

---

# Objective

This document describes the network configuration implemented within the pfSense firewall home lab. It covers interface addressing, gateway configuration, DHCP services, DNS forwarding, and connectivity verification.

The goal was to establish reliable communication between the internal LAN and external network while ensuring that all outbound traffic passed through the pfSense firewall.

---

# Network Overview

The lab consists of two Layer 3 networks:

| Network | Address Space | Purpose |
|----------|---------------|---------|
| WAN | 10.0.2.0/24 | External Network |
| LAN | 192.168.10.0/24 | Internal Trusted Network |

The pfSense firewall routes traffic between these two networks.

---

# WAN Configuration

| Setting | Value |
|----------|-------|
| Interface | em0 |
| Address | 10.0.2.15/24 |
| Gateway | 10.0.2.2 |
| Network | 10.0.2.0/24 |

## Purpose

The WAN interface connects the firewall to the VirtualBox NAT router, providing Internet access for internal hosts.

The default gateway (10.0.2.2) forwards traffic destined for external networks.

---

# LAN Configuration

| Setting | Value |
|----------|-------|
| Interface | em1 |
| Address | 192.168.10.1/24 |
| Network | 192.168.10.0/24 |

## Purpose

The LAN interface acts as the default gateway for internal systems.

All traffic originating from the LAN must pass through this interface before reaching external destinations.

---

# DHCP Configuration

DHCP was enabled on the LAN interface to automatically assign IP addresses and network configuration to internal hosts.

The DHCP server provides:

- IP Address
- Subnet Mask
- Default Gateway
- DNS Server

This removes the need for manual network configuration on client systems.

---

# DNS Configuration

The pfSense firewall was configured to act as a DNS forwarder.

Internal clients send DNS requests to the firewall.

The firewall then forwards those requests to upstream DNS servers.

This provides:

- Centralized DNS management
- Faster repeat lookups through caching (when enabled)
- Simplified client configuration

---

# Default Gateway

The Ubuntu Server uses:

| Setting | Value |
|----------|-------|
| Default Gateway | 192.168.10.1 |

When the destination address is outside the local subnet, packets are forwarded to the pfSense LAN interface for routing.

---

# Routing Process

The packet forwarding process is summarized below.

```text
Ubuntu Server
        │
Destination outside LAN?
        │
        ▼
Default Gateway
192.168.10.1
        │
        ▼
pfSense Routing Table
        │
        ▼
Firewall Rules
        │
        ▼
Source NAT
        │
        ▼
WAN Interface
        │
        ▼
Internet
```

---

# Design Decisions

## Why use DHCP?

DHCP reduces manual configuration and minimizes addressing errors.

---

## Why use pfSense for DNS?

Using the firewall as the DNS forwarder centralizes name resolution and simplifies client configuration.

---

## Why use a separate LAN subnet?

Separating internal and external networks allows firewall rules, routing decisions, and NAT behavior to be tested in a controlled environment.

---

# Verification

The network configuration was verified using the following methods:

- Successful DHCP lease assignment
- Ping to 192.168.10.1
- Ping to 8.8.8.8
- Ping to google.com
- DNS Lookup
- Routing Table
- Packet Capture

These tests confirmed that addressing, routing, DNS resolution, and Internet connectivity were functioning correctly.

---

# Screenshots

Include:

- WAN Interface Configuration
- LAN Interface Configuration
- DHCP Server Configuration
- DNS Resolver / Forwarder Configuration
- Successful ping to 8.8.8.8
- Successful ping to google.com

---

# Key Takeaways

The network configuration established a functional Layer 3 environment where the pfSense firewall served as the gateway, DHCP server, DNS forwarder, and routing device.

This configuration forms the foundation for firewall policy enforcement, Network Address Translation (NAT), packet analysis, and troubleshooting throughout the remainder of the project.