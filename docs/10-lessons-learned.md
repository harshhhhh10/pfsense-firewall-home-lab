# Lessons Learned

---

# Project Reflection

This project was designed to move beyond theoretical networking concepts by implementing and validating a firewall in a controlled virtual environment.

Rather than treating pfSense as a black-box appliance, every major networking function was observed, tested, and verified using built-in diagnostic tools and packet analysis.

The project demonstrated that successful firewall administration requires understanding both configuration and the underlying network behavior.

---

# Networking Concepts Reinforced

## IP Addressing

This project reinforced the distinction between private and routable IP addressing.

Internal systems communicated using the private network:

```
192.168.10.0/24
```

while the firewall translated traffic to its WAN address before forwarding packets to external networks.

---

## Routing

The routing table determines where packets are forwarded.

Understanding the default route made it clear how unknown destinations are forwarded toward the upstream gateway.

---

## Network Address Translation (NAT)

One of the most valuable lessons was observing Source NAT through packet captures.

Instead of simply reading about NAT, I verified that:

```
192.168.10.100
```

became

```
10.0.2.15
```

on the WAN interface.

This demonstrated how private networks communicate with external systems.

---

## Stateful Firewall Operation

The project reinforced that pfSense is a stateful firewall.

Outbound connections automatically created state entries, allowing reply traffic without requiring separate inbound rules.

Understanding stateful inspection changed how firewall rules were interpreted during testing.

---

## Firewall Rule Evaluation

The lab confirmed that firewall rules are processed using a first-match model.

An intentionally created ICMP block rule demonstrated how rule order directly affects network behavior.

Firewall logs confirmed which rule processed each packet.

---

## Packet Analysis

Packet captures provided evidence for:

- ICMP communication
- DNS requests
- NAT translation
- HTTP traffic
- HTTPS traffic

Packet analysis became one of the most effective methods for verifying firewall behavior.

---

## Diagnostics

Built-in diagnostic tools such as:

- Ping
- Traceroute
- DNS Lookup
- ARP Table
- Routing Table
- State Table

provided practical insight into how different networking components interact.

Rather than relying on assumptions, each tool was used to verify a specific aspect of the environment.

---

# Engineering Mindset

One of the most important lessons from this project was learning to verify configurations rather than assuming they were correct.

When issues occurred, they were investigated using logs, packet captures, and diagnostic tools before making configuration changes.

This structured troubleshooting process reduced unnecessary changes and helped identify root causes more efficiently.

---

# Challenges Encountered

Several practical challenges were encountered during the implementation:

- Firewall rules affecting expected connectivity
- Interpreting packet captures containing background traffic
- Understanding first-match firewall processing
- Understanding why NAT changes only the source address
- Distinguishing routing issues from DNS issues

Each challenge improved practical understanding of enterprise firewall behavior.

---

# Skills Developed

This project strengthened practical experience in:

### Networking

- IPv4 Addressing
- Routing
- Default Gateway
- DNS
- ARP
- ICMP

### Firewall Administration

- Stateful Packet Inspection
- Firewall Rule Management
- NAT Configuration
- Logging
- Diagnostics

### Troubleshooting

- Packet Analysis
- Firewall Log Analysis
- Connectivity Testing
- Root Cause Investigation
- Verification Methodology

---

# Future Improvements

This firewall lab provides the networking foundation for future cybersecurity projects.

Planned projects include:

1. Active Directory Lab
2. Windows Event Forwarding
3. Sysmon Deployment
4. Wazuh SIEM
5. Detection Engineering
6. Threat Hunting
7. Incident Response

Each project will build upon the networking and firewall concepts established in this repository.

---

# Final Thoughts

Completing this project transformed networking concepts from theory into practical experience.

Instead of only configuring a firewall, I learned how to observe, verify, troubleshoot, and document network behavior using evidence gathered throughout the implementation.

These skills provide a solid foundation for future work in system administration, security operations, detection engineering, and incident response.