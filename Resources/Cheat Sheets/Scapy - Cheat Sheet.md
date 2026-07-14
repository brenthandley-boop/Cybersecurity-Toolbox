# Scapy Cheat Sheet
**Packet Manipulation & Network Programming — Quick Reference**

---

## Core Workflow

1. Import Scapy in an interactive Python shell or script
2. Build a packet, layer by layer
3. Send, sniff, or send-and-receive
4. Inspect the result
5. Save/export if needed for later analysis

---

## Setup

```python
from scapy.all import *
```

---

## Building Packets (Layering)

| Syntax | Result |
|---|---|
| `IP(dst="192.168.1.10")` | Basic IP layer |
| `IP(dst="192.168.1.10")/ICMP()` | IP + ICMP (ping-style packet) |
| `IP(dst="192.168.1.10")/TCP(dport=80, flags="S")` | IP + TCP SYN to port 80 |
| `Ether()/IP()/UDP()` | Full Layer 2–4 stack (Ethernet + IP + UDP) |
| `pkt[TCP].flags = "A"` | Modify a field on an existing packet object |

---

## Sending & Receiving

| Function | Behavior |
|---|---|
| `send(pkt)` | Send at Layer 3 (OS handles routing/Ethernet) |
| `sendp(pkt)` | Send at Layer 2 (you control Ethernet framing) |
| `sr(pkt)` | Send and receive — returns (answered, unanswered) lists |
| `sr1(pkt)` | Send and receive — returns only the first response |
| `srp(pkt)` | Layer 2 version of `sr()` |

---

## Sniffing

| Command | Purpose |
|---|---|
| `sniff(count=10)` | Capture 10 packets |
| `sniff(filter="tcp port 80")` | Capture with a BPF-style filter |
| `sniff(prn=lambda p: p.summary())` | Run a custom function on each captured packet |
| `sniff(iface="eth0")` | Capture on a specific interface |

---

## Inspecting Packets

| Command | Purpose |
|---|---|
| `pkt.show()` | Full layered breakdown of a packet |
| `pkt.summary()` | One-line summary |
| `pkt[IP].src` / `pkt[IP].dst` | Access a specific field |
| `hexdump(pkt)` | Raw hex view of the packet |
| `ls(IP)` | List all fields available on a layer |

---

## pcap File Operations

| Command | Purpose |
|---|---|
| `wrpcap("file.pcap", pkt)` | Write packet(s) to a pcap file |
| `rdpcap("file.pcap")` | Read packets from a pcap file into a list |

---

## Common Patterns

### Custom TCP SYN Scan

```python
ans, unans = sr(IP(dst="192.168.1.10")/TCP(dport=(1, 1024), flags="S"), timeout=2)
ans.summary()
```

### ARP Ping (Layer 2 host discovery)

```python
ans, unans = arping("192.168.1.0/24")
```

### Traceroute

```python
res, unans = traceroute("192.168.1.10")
```

### DNS Query

```python
pkt = IP(dst="8.8.8.8")/UDP(dport=53)/DNS(rd=1, qd=DNSQR(qname="example.com"))
response = sr1(pkt)
```

---

## Pro Tips

- **`sr1()` for one answer, `sr()` for a full set** — using the wrong one silently drops data you actually wanted.
- **Raw socket operations require root/admin privileges** — expect permission errors otherwise, especially for `sendp()`/`srp()`.
- **`pkt.show()` is the fastest way to debug a malformed packet** — it reveals exactly which fields Scapy actually set versus assumed defaults.
- **Set a `timeout` on `sr()`/`sr1()` calls** — without one, Scapy can hang indefinitely waiting for a response that isn't coming.
- **Combine with Wireshark for verification** — capture on the target side while sending from Scapy to confirm the packet arrived exactly as built.
