# Network Diagnostics

---

# Objective

This document explains the diagnostic tools used throughout the pfSense home lab to validate network connectivity, routing, name resolution, and firewall operation.

Rather than assuming the firewall was configured correctly, each component was tested using built-in diagnostic utilities and verified through observable results.

---

# Why Network Diagnostics Matter

Network diagnostics help administrators answer critical questions:

- Can devices communicate?
- Is routing functioning correctly?
- Is DNS resolving hostnames?
- Which path does traffic follow?
- Is the firewall forwarding packets?
- Where is communication failing?

Each tool provides a different perspective into network behavior.

---

# Ping

## Purpose

Ping verifies Layer 3 connectivity between hosts using the ICMP protocol.

## Lab Verification

The following tests were performed:

- Ping pfSense LAN Interface
- Ping 8.8.8.8
- Ping google.com

## Observations

Successful replies confirmed:

- LAN connectivity
- Internet connectivity
- DNS functionality (when using hostnames)

---

# Traceroute

## Purpose

Traceroute identifies the path packets take toward a destination.

It also helps identify where communication stops.

## Lab Verification

Traceroute was executed against:

```
google.com
```

## Observations

The first hop reached the VirtualBox NAT gateway.

Several later hops returned:

```
* * *
```

This behavior is expected because many Internet routers do not respond to traceroute probes for security or performance reasons.

---

# DNS Lookup

## Purpose

DNS Lookup verifies hostname resolution.

## Lab Verification

Hostname tested:

```
google.com
```

## Observations

The lookup returned:

- IPv4 (A) Record
- IPv6 (AAAA) Records

The firewall also displayed response times from configured DNS servers.

This confirmed that DNS forwarding was operating correctly.

---

# ARP Table

## Purpose

ARP maps IPv4 addresses to MAC addresses within the local network.

## Lab Verification

The ARP table showed entries for:

- pfSense LAN
- Ubuntu Server
- WAN Gateway

## Observations

No ARP entry existed for remote Internet hosts such as 8.8.8.8 because ARP operates only within the local broadcast domain.

Traffic destined for remote networks is sent to the default gateway instead.

---

# Routing Table

## Purpose

The routing table determines where packets are forwarded.

## Lab Verification

The routing table confirmed:

- Default Route
- WAN Network
- LAN Network
- Loopback Interface

## Observations

Unknown destinations were forwarded through:

```
10.0.2.2
```

using the default route.

---

# State Table

## Purpose

The state table tracks active connections.

It allows reply traffic without requiring additional inbound firewall rules.

## Lab Verification

Active connections were observed during:

- Ping
- HTTPS
- DNS

## Observations

Reply packets were successfully matched against existing firewall states.

This demonstrated Stateful Packet Inspection (SPI).

---

# Verification Summary

| Diagnostic Tool | Verified |
|-----------------|----------|
| Ping | Connectivity |
| Traceroute | Packet Path |
| DNS Lookup | Name Resolution |
| ARP Table | Local Address Resolution |
| Routing Table | Packet Forwarding |
| State Table | Stateful Inspection |

---

# Screenshots

Include:

- Ping to 8.8.8.8
- Ping to google.com
- Traceroute
- DNS Lookup
- ARP Table
- Routing Table
- State Table

---

# Key Takeaways

Each diagnostic tool provided evidence for a different networking function.

Rather than relying on assumptions, these utilities confirmed connectivity, routing, DNS resolution, local address resolution, and firewall state tracking throughout the lab.