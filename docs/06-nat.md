# Network Address Translation (NAT)

---

# Objective

This document explains how Network Address Translation (NAT) was configured and verified within the pfSense firewall home lab.

The objective was to understand how pfSense translates private IP addresses into routable addresses, how outbound NAT rules are evaluated, and how packet captures can be used to verify the translation process.

---

# What is NAT?

Network Address Translation (NAT) modifies IP addresses as packets pass through the firewall.

In this lab, Ubuntu Server uses a private IPv4 address:

```

192.168.10.100

```

This address is not routable on the Internet.

Before packets leave the WAN interface, pfSense translates the source address into the WAN interface address:

```

192.168.10.100
↓

10.0.2.15

```

This process is called **Source NAT (SNAT)** or **Port Address Translation (PAT)**.

---

# Why NAT is Required

Private IPv4 addresses (RFC 1918) cannot be routed across the public Internet.

Without NAT:

- External hosts would not know how to return traffic.
- Private addresses would be discarded by upstream routers.

NAT allows internal systems to communicate with external networks using the firewall's WAN address.

---

# NAT Modes in pfSense

pfSense supports multiple outbound NAT modes.

## Automatic Outbound NAT

pfSense automatically creates translation rules based on connected networks.

Advantages:

- Simple configuration
- Suitable for most environments
- Automatically updates when interfaces change

---

## Hybrid Outbound NAT

Hybrid mode combines automatic rules with manually created rules.

This allows custom translations while retaining automatically generated rules.

---

## Manual Outbound NAT

Manual mode gives complete control over every translation rule.

All outbound NAT rules must be managed manually.

This mode is commonly used in enterprise environments requiring granular control.

---

# NAT Configuration Used

This project demonstrated manual outbound NAT by creating a rule specifically for the Ubuntu Server.

| Setting | Value |
|----------|-------|
| Source | 192.168.10.100/32 |
| Translation | WAN Address |
| Interface | WAN |
| Protocol | Any |

The rule translates traffic originating from Ubuntu Server to the WAN interface address before forwarding packets to the Internet.

---

# Rule Evaluation

Outbound NAT rules are processed from top to bottom.

The first matching rule is applied.

```

Packet
│
▼
Rule 1 → Match? → YES → Translate → Stop

NO

▼
Rule 2

```

Rule order is therefore critical when multiple NAT rules exist.

---

# NAT Verification

NAT was verified using packet captures on both LAN and WAN interfaces.

## LAN Packet Capture

Observed:

| Source | Destination |
|---------|-------------|
| 192.168.10.100 | 8.8.8.8 |

This confirms that packets leave Ubuntu using its private IP address.

---

## WAN Packet Capture

Observed:

| Source | Destination |
|---------|-------------|
| 10.0.2.15 | 8.8.8.8 |

The source address changed from:

```

192.168.10.100

```

to

```

10.0.2.15

```

This confirms that Source NAT was successfully applied.

---

# Packet Flow

```

Ubuntu Server
192.168.10.100
│
▼
LAN Interface
│
▼
Firewall Rule Evaluation
│
▼
State Creation
│
▼
Source NAT (PAT)
192.168.10.100
↓

10.0.2.15
│
▼
WAN Interface
│
▼
Internet

```

Return traffic follows the reverse path and is mapped back to the original internal host using the firewall's state table.

---

# Design Decisions

## Why use Source NAT?

Source NAT allows multiple internal devices to share a single WAN IP address while maintaining independent connections.

---

## Why verify on both interfaces?

Capturing packets on both LAN and WAN interfaces provides direct evidence that translation occurred.

Configuration alone does not prove NAT is functioning correctly.

---

## Why use packet captures?

Packet captures reveal the actual packets processed by the firewall, making them one of the most reliable methods for validating network behavior.

---

# Screenshots

Include the following screenshots:

- Outbound NAT Overview
- Manual NAT Rule
- Automatic NAT Rules
- LAN Packet Capture (Before NAT)
- WAN Packet Capture (After NAT)

---

# Key Takeaways

This phase demonstrated:

- Private vs public addressing
- Source NAT (SNAT)
- Port Address Translation (PAT)
- Outbound NAT rule processing
- First-match evaluation
- Packet capture verification

Understanding NAT is fundamental for firewall administration because nearly all outbound Internet communication depends on accurate address translation.