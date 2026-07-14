# Scapy — Packet Manipulation & Network Programming

**Category:** Packet Crafting & Network Automation (Python Library)
**Difficulty:** Intermediate to Advanced
**License:** Open Source (GPLv2)

---

## Description

Scapy is a Python-based interactive packet manipulation library that lets you craft, send, sniff, dissect, and forge network packets at a granular level. Where Wireshark analyzes traffic that already exists, Scapy builds traffic from scratch — making it a core tool for testing detection rules, understanding protocols at a deep level, and automating custom network tools that off-the-shelf software doesn't support.

Security professionals use Scapy daily for:

- Crafting custom packets to test firewall and IDS/IPS rules (including Snort rules)
- Protocol fuzzing and edge-case testing
- Building lightweight, purpose-specific scanning or recon tools
- Automating network testing tasks as part of a larger Python script or pipeline

---

## Key Features

- Interactive Python shell for building and manipulating packets layer by layer
- Broad built-in protocol support (IP, TCP, UDP, ICMP, ARP, DNS, and many more)
- Combined send/receive functions (`sr`, `sr1`) for request/response workflows
- Full packet dissection and inspection via simple, layered syntax
- Native pcap read/write support
- Integrates directly into larger Python scripts and automation pipelines

---

## Common Commands

### Basic Setup

```python
from scapy.all import *
```

### Building and Sending Packets

```python
# Build a layered packet: IP + ICMP
pkt = IP(dst="192.168.1.10")/ICMP()

# Send at Layer 3 (routing handled by OS)
send(pkt)

# Send at Layer 2 (requires specifying interface/destination MAC)
sendp(pkt)

# Send and capture a single response
response = sr1(pkt)
```

### Inspecting Packets

```python
# Display a packet's full layered structure
pkt.show()

# Print a one-line summary
pkt.summary()
```

### Sniffing Traffic

```python
# Sniff 10 packets
sniff(count=10)

# Sniff with a filter and a custom handler function
sniff(filter="tcp port 80", prn=lambda p: p.summary())
```

### Working with pcap Files

```python
# Write packets to a pcap file
wrpcap("capture.pcap", pkt)

# Read packets from a pcap file
packets = rdpcap("capture.pcap")
```

### Example: Custom TCP SYN Scan

```python
ans, unans = sr(IP(dst="192.168.1.10")/TCP(dport=(1, 1024), flags="S"), timeout=2)
ans.summary()
```

---

## Hands-On Learning Path

Scapy proficiency comes from understanding protocol structure well enough to build valid (and deliberately invalid) packets on purpose — not from copy-pasting scripts. Below is the progression most cybersecurity students use to build reps, entirely within isolated lab environments.

**Guided / official starting points**
- [ ] Scapy's official usage documentation and interactive tutorial
- [ ] Reviewing RFC-level protocol structure (e.g., TCP/IP headers) alongside Scapy's layer syntax, to connect theory to code

**Home lab (VirtualBox / isolated network)**
- [ ] Crafting and sending a basic ICMP packet to a lab host, confirming receipt in Wireshark on the target side
- [ ] Building a custom TCP SYN scanner in Scapy and comparing results against an equivalent Nmap scan
- [ ] Crafting a malformed or edge-case packet to observe how a lab target (or Snort instance) responds

**Applied / integration practice**
- [ ] Writing a small Python script that combines Scapy-based packet generation with basic scan logic, as a custom recon tool
- [ ] Using Scapy to generate test traffic that validates a custom Snort or Wazuh detection rule — closing the loop between "detection written" and "detection confirmed"

---

## Best Practices

- **Only craft and send packets in authorized lab environments.** Crafted traffic can bypass normal validation and produce unpredictable behavior on systems you don't control.
- **Understand the protocol before crafting the packet.** Scapy will happily build a technically invalid packet — knowing *why* it's invalid is the actual learning objective.
- **Expect to need elevated privileges.** Raw socket access (required for most Scapy operations) typically requires root/administrator privileges — a good reminder of how sensitive this capability is.
- **Use sparingly against production or shared networks.** Malformed or unusual traffic can trigger unintended side effects beyond just detection alerts.
- **Document crafted packet structure in any script you write.** A packet-crafting script without comments explaining the intended layers/flags is very hard for anyone (including future you) to audit.

---

## Most Valuable Lessons Learned *(in progress)*

This section will grow with real findings as labs above are completed. Early conceptual takeaway:

- **Scapy makes protocol theory concrete.** Building a packet layer-by-layer in Python is a fundamentally different (and more durable) way of learning TCP/IP than reading about header fields in the abstract.

I'd rather keep this honest and incremental than pad it — real scripts and findings will replace this note as work is completed.

---

## Resources

- [Scapy Official Documentation](https://scapy.readthedocs.io/)
- [Scapy GitHub Repository](https://github.com/secdev/scapy)
- [RFC 793 — TCP Protocol Specification](https://datatracker.ietf.org/doc/html/rfc793) *(useful reference alongside Scapy's TCP layer)*
