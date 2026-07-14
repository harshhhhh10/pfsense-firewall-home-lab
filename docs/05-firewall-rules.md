# Firewall Rules

---

# Objective

This document explains how firewall rules were implemented and validated within the pfSense home lab.

The primary objective was to understand how pfSense evaluates traffic, applies security policies, creates state entries, and permits or blocks network communication.

---

# Firewall Philosophy

pfSense follows a **default deny** security model.

Traffic is denied unless an explicit firewall rule allows it.

This approach follows the principle of least privilege by permitting only the traffic that is required.

---

# Rule Evaluation

Firewall rules are processed from the top of the list to the bottom.

The first rule that matches a packet is immediately applied.

Subsequent rules are not evaluated.

```
Packet
   │
   ▼
Rule 1 → Match? → YES → Stop Processing
                  │
                  NO
                  ▼
Rule 2
                  │
                  ▼
Rule 3
```

Because of this first-match behavior, rule order is critical.

---

# Implemented Rules

## Allow LAN Traffic

Purpose:

Allow trusted internal hosts to initiate outbound connections.

Result:

- Internet connectivity
- DNS resolution
- Web browsing
- ICMP testing

---

## Block HTTP Rule

Purpose:

Prevent internal systems from accessing unencrypted HTTP websites.

Reason:

HTTP transmits data in plaintext.

HTTPS provides encryption and authentication.

---

## Manual Outbound NAT Rule

Purpose:

Apply Source NAT only for the Ubuntu Server.

Source:

192.168.10.100/32

Translation:

WAN Address

This rule demonstrated first-match processing within the Outbound NAT rule set.

---

# Stateful Packet Inspection

pfSense is a stateful firewall.

When an internal host initiates a connection:

1. Firewall rule is evaluated.
2. State entry is created.
3. Reply traffic is automatically permitted.
4. State is removed after the session expires.

No additional inbound WAN rule is required for reply traffic.

---

# Rule Verification

Each firewall rule was validated using one or more methods:

- Firewall Logs
- Packet Capture
- State Table
- Successful Ping
- Blocked HTTP Requests

Verification confirmed that traffic matched the intended rule and that first-match processing behaved as expected.

---

# Firewall Logs

Firewall logs were used to confirm:

- Rule ID
- Source Address
- Destination Address
- Interface
- Protocol
- Action (Pass / Block)

Blocked HTTP requests appeared in the logs exactly as expected after the rule was implemented.

---

# Design Decisions

## Why block HTTP?

HTTP traffic is transmitted without encryption.

Blocking HTTP encourages secure communication using HTTPS.

---

## Why allow LAN before WAN?

Internal hosts are trusted to initiate outbound connections.

External hosts should not be allowed to initiate unsolicited inbound connections.

---

## Why verify using logs?

Firewall logs provide evidence that traffic matched the expected rule.

Configuration alone does not prove that a rule is functioning correctly.

---

# Screenshots

Include:

- LAN Firewall Rules
- HTTP Block Rule
- Firewall Log showing blocked HTTP traffic
- State Table after successful HTTPS connection

---

# Key Takeaways

This phase demonstrated several core firewall concepts:

- Default deny security
- First-match rule evaluation
- Stateful packet inspection
- Traffic logging
- Rule verification

These concepts form the foundation of enterprise firewall administration.