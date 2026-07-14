# Project Overview

---

# Objective

The objective of this project was to design, implement, and validate a production-inspired firewall using **pfSense Community Edition** within a virtual home lab. Rather than focusing solely on installation, the project emphasizes understanding how enterprise firewalls inspect, process, and secure network traffic.

Throughout the implementation, every major configuration was verified using pfSense's built-in diagnostic tools, firewall logs, packet captures, routing tables, and state tables to reinforce practical networking concepts.

---

# Problem Statement

Modern enterprise environments rely on firewalls as the primary security boundary between trusted internal networks and untrusted external networks. Simply deploying a firewall is insufficient—security professionals must understand how traffic flows through it, how policies are evaluated, and how network services interact.

This project was created to build that practical understanding through hands-on implementation and testing.

---

# Goals

The project was designed with the following goals:

- Deploy a functional pfSense firewall.
- Configure WAN and LAN interfaces.
- Provide network connectivity for internal hosts.
- Configure DHCP and DNS services.
- Implement firewall security policies.
- Configure Network Address Translation (NAT).
- Capture and analyze network packets.
- Understand Stateful Packet Inspection (SPI).
- Investigate routing decisions.
- Troubleshoot common networking issues.
- Produce professional technical documentation.

---

# Lab Environment

| Component | Description |
|-----------|-------------|
| Firewall | pfSense Community Edition |
| Hypervisor | Oracle VirtualBox |
| Internal Host | Ubuntu Server |
| External Network | VirtualBox NAT |
| Internal Network | 192.168.10.0/24 |
| WAN Network | 10.0.2.0/24 |

---

# Technologies Used

- pfSense CE
- Oracle VirtualBox
- Ubuntu Server
- DHCP
- DNS
- ICMP
- TCP/IP
- NAT
- Packet Capture
- Firewall Logging

---

# Project Scope

This project covers the following areas:

- Firewall deployment
- Interface configuration
- DHCP configuration
- DNS configuration
- Firewall rule creation
- Outbound NAT
- Port Forwarding
- Packet Capture
- Firewall Logs
- Routing Table Analysis
- ARP Table Analysis
- State Table Analysis
- Network Diagnostics
- Backup & Restore
- Basic CLI Administration

The project does not include enterprise features such as High Availability (HA), VPN deployments, VLAN segmentation, IDS/IPS, or multi-site routing. Those topics will be explored in future projects.

---

# Learning Outcomes

After completing this project, I gained practical experience with:

- Firewall administration
- Network Address Translation (NAT)
- Routing fundamentals
- ARP resolution
- Stateful Packet Inspection
- Packet analysis
- Firewall troubleshooting
- Network diagnostics
- Configuration backup and recovery

More importantly, this project helped connect theoretical networking concepts with practical firewall behavior through repeated testing and verification.

---

# Verification Approach

Rather than assuming configurations were correct, every implementation was validated using one or more of the following:

- Firewall Logs
- Packet Capture
- Ping
- Traceroute
- DNS Lookup
- ARP Table
- Routing Table
- State Table

This verification-first approach ensured that every configuration change produced the expected networking behavior.

---

# Conclusion

This project establishes the networking and firewall foundation for a larger cybersecurity home lab. The knowledge gained here will support future projects involving VLAN segmentation, Active Directory, SIEM deployment, detection engineering, and incident response.