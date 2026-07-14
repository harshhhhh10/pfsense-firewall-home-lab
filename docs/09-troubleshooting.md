# Troubleshooting

---

# Objective

This document records the main connectivity and firewall issues encountered during the pfSense home lab and explains how each issue was investigated and resolved.

The purpose of this section is to demonstrate a structured troubleshooting process rather than presenting only the final working configuration.

---

# Troubleshooting Methodology

The following sequence was used throughout the lab:

```text
Physical / Virtual Interface
        ↓
IP Addressing
        ↓
Default Gateway
        ↓
Routing
        ↓
Firewall Rules
        ↓
NAT
        ↓
DNS
        ↓
Application
```

This order prevents unnecessary configuration changes and helps isolate the failing layer.

---

# Case 1 — DNS Resolution Failure

## Symptoms

Ubuntu could reach external IP addresses such as:

```text
8.8.8.8
```

but could not resolve hostnames such as:

```text
google.com
```

The system returned:

```text
Temporary failure in name resolution
```

## Investigation

The following tests were performed:

```bash
ping -c 4 8.8.8.8
```

This succeeded, proving that:

- The interface was active.
- The default gateway was reachable.
- Routing and Internet connectivity were working.

The next test was:

```bash
nslookup google.com 192.168.10.1
```

The request timed out.

The pfSense DNS diagnostic page showed that external resolvers such as `1.1.1.1` and `8.8.8.8` responded, while the local resolver did not.

## Root Cause

Ubuntu was configured to use pfSense as its DNS server, but the local DNS service was not responding correctly.

## Resolution

The pfSense DNS configuration was reviewed and upstream DNS servers were configured.

The network connection was then renewed and DNS was tested again.

## Verification

```bash
ping -c 4 google.com
```

and:

```bash
nslookup google.com
```

returned valid IP addresses.

## Lesson

Successful communication with an IP address does not prove that DNS is working.

---

# Case 2 — ICMP Blocked by Firewall Policy

## Symptoms

Ubuntu could not ping the pfSense LAN interface:

```text
192.168.10.1
```

The result showed:

```text
100% packet loss
```

## Investigation

Ubuntu had the expected address:

```text
192.168.10.100/24
```

The pfSense LAN interface was also active:

```text
192.168.10.1/24
```

The firewall logs showed:

```text
Rule: Block ICMP from LAN
Source: 192.168.10.100
Destination: 192.168.10.1
Protocol: ICMP
Action: Block
```

## Root Cause

The ICMP block rule appeared above the default LAN allow rule.

Because pfSense processes rules from top to bottom, the ICMP rule matched first and processing stopped.

## Resolution

The ICMP block rule was temporarily disabled while connectivity testing and screenshot collection were performed.

## Verification

After disabling the rule:

```bash
ping 192.168.10.1
```

returned successful replies.

## Lesson

Rule order is critical. A broad or specific block rule placed above an allow rule can change connectivity immediately.

---

# Case 3 — Traceroute Returned `* * *`

## Symptoms

Traceroute showed the first hop:

```text
10.0.2.2
```

but later hops displayed:

```text
* * *
```

## Investigation

Other tests were successful:

- Ping to `8.8.8.8`
- Ping to `google.com`
- DNS Lookup
- Gateway status

## Root Cause

Intermediate routers or the VirtualBox NAT environment did not return traceroute responses.

This does not necessarily mean that packets were not forwarded.

## Resolution

No configuration change was required.

The traceroute output was interpreted together with other diagnostic evidence.

## Lesson

A missing traceroute response does not automatically prove a connectivity failure.

---

# Case 4 — New Firewall Rule Did Not Appear to Work

## Symptoms

A newly created firewall rule did not immediately affect traffic.

## Investigation

pfSense maintains connection states for active sessions.

An existing state may continue to permit traffic even after the firewall policy changes.

## Root Cause

The traffic may have matched a state created before the rule was added or changed.

## Resolution

The relevant state was allowed to expire or was cleared from:

```text
Diagnostics → States
```

The traffic was then generated again.

## Lesson

Firewall rule changes generally affect new connections. Existing states may need to be cleared during testing.

---

# Case 5 — Excessive Packet Capture Noise

## Symptoms

WAN packet captures contained many unrelated packets, including:

- ICMP gateway monitoring
- IPv6 link-local traffic
- DNS traffic
- NTP traffic

This made it difficult to identify the test traffic.

## Investigation

The capture had been performed with a broad filter.

## Root Cause

pfSense and the surrounding environment continuously generate normal background traffic.

## Resolution

More specific capture filters were used:

- Interface: WAN
- Address Family: IPv4
- Protocol: ICMP
- Host: `8.8.8.8`
- Limited packet count

## Verification

The resulting capture clearly showed the intended ICMP Echo Requests and Echo Replies.

## Lesson

Packet capture filters reduce noise and make investigation faster and more reliable.

---

# Troubleshooting Decision Tree

```text
Cannot access a service
        │
        ▼
Does the interface have an IP?
        │
   No ──┴── Yes
   │          │
Fix DHCP      Can it reach the gateway?
or static IP  │
          No ─┴─ Yes
          │      │
Check virtual Check external IP
network / ARP │
              ▼
        Can it reach 8.8.8.8?
              │
         No ──┴── Yes
         │          │
Check route,     Test hostname
firewall, NAT    resolution
                    │
               No ──┴── Yes
               │          │
            Check DNS   Check application
```

---

# Evidence Used

The following sources were used during troubleshooting:

- Firewall Logs
- Packet Captures
- Interface Status
- Ping
- Traceroute
- DNS Lookup
- ARP Table
- Routing Table
- State Table

---

# Key Takeaways

The most important troubleshooting lessons were:

- Test IP connectivity before diagnosing DNS.
- Check firewall logs before changing rules.
- Rule order can explain unexpected blocks.
- Stateful firewalls may preserve existing sessions.
- Traceroute must be interpreted alongside other evidence.
- Narrow packet capture filters improve analysis.
- Configuration should be verified through observable results.