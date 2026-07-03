# Wireshark — Network Protocol Analyzer

**Category:** Traffic Analysis & Packet Inspection
**Difficulty:** Beginner to Intermediate
**License:** Open Source (GPL)

---

## Description

Wireshark is the industry-standard tool for capturing and analyzing network traffic at the packet level. Where a tool like Nmap tells you what exists on a network, Wireshark tells you what's actually happening on it — every packet, every protocol, every conversation, in real time or from a saved capture.

Security professionals use Wireshark daily for:

- Incident investigation and forensic analysis
- Malware traffic and command-and-control (C2) detection
- Validating and enriching SIEM/IDS alerts with ground-truth packet data
- Troubleshooting network performance and connectivity issues
- Learning and teaching how protocols actually behave on the wire

---

## Key Features

- Live packet capture and offline analysis (`.pcap`/`.pcapng` files)
- Capture filters (limit what's recorded) and display filters (narrow what's viewed)
- Deep protocol dissection (HTTP, DNS, TCP/IP, ARP, DHCP, TLS, and hundreds more)
- "Follow Stream" — reconstructing a full conversation from individual packets
- Statistics tools (conversations, protocol hierarchy, I/O graphs)
- Color-coding rules to visually flag traffic types or anomalies
- `tshark` — the command-line version, for scripting and automation

---

## Common Commands

### Capture Filters (set before capture starts)

```
# Capture traffic only to/from a specific host
host 192.168.1.5

# Capture only HTTP (port 80) traffic
tcp port 80

# Capture traffic on a specific subnet
net 192.168.1.0/24
```

### Display Filters (applied after capture, in the GUI filter bar)

```
# Show only HTTP requests
http.request

# Show only SYN packets (connection attempts)
tcp.flags.syn==1 && tcp.flags.ack==0

# Show traffic to/from a specific IP
ip.addr == 192.168.1.105

# Show DNS queries
dns.flags.response == 0
```

### tshark (command-line capture)

```bash
# Capture 100 packets on interface eth0
tshark -i eth0 -c 100

# Capture and save to a file
tshark -i eth0 -w capture.pcapng

# Read a saved capture and apply a display filter
tshark -r capture.pcapng -Y "http.request"
```

---

## Hands-On Learning Path

Wireshark proficiency comes from reading real (or realistic) traffic, not memorizing filter syntax. Below is the progression most cybersecurity students and self-taught practitioners use to build reps. Checked items reflect captures actually analyzed; this list updates as real work is done.

**Public, purpose-built practice captures**
- [ ] Wireshark's official [Sample Captures](https://wiki.wireshark.org/SampleCaptures) — pre-made `.pcap` files covering common protocols
- [ ] [Malware-Traffic-Analysis.net](https://www.malware-traffic-analysis.net/) exercises — real (defanged) malware capture analysis with write-ups to check your work against
- [ ] TryHackMe "Wireshark: The Basics," "Wireshark: Packet Operations," and "Wireshark: Traffic Analysis" rooms — guided, scored exercises

**Home lab (VirtualBox / isolated network)**
- [x] Live capture and filtering on an isolated lab network
- [x] Following a full TCP stream to reconstruct an HTTP request/response
- [x] Filtering out ARP/broadcast noise to isolate traffic of interest
- [ ] Capturing and analyzing a DNS exfiltration or tunneling simulation
- [ ] Capturing my own Nmap scan from the target side, to see what a scan actually looks like on the wire

**Applied / integration practice**
- [ ] Correlating a Wireshark capture with corresponding Splunk log entries for the same event
- [ ] Practicing a full "alert to packet capture" workflow — starting from a simulated SIEM alert and tracing it back to raw traffic

---

## Best Practices

- **Filter with intent, not curiosity.** Live networks generate huge volumes of background noise (ARP, broadcast traffic) — build filters around a specific question you're trying to answer rather than scrolling raw captures.
- **Capture only what you're authorized to see.** Packet capture can expose sensitive data (credentials, PII) — this makes scope and authorization even more important than with a scanning tool like Nmap.
- **Use capture filters to manage volume, display filters to analyze.** Capturing everything and filtering later is fine for short lab sessions, but on busy networks it can produce unmanageably large files.
- **Learn to read a TCP handshake fluently.** Recognizing a normal SYN → SYN-ACK → ACK sequence makes it immediately obvious when something (a scan, a reset, a failed connection) deviates from it.
- **Correlate with other data sources.** Wireshark shows you the wire-level truth, but pairing it with logs (e.g., from Splunk) gives you both the "what happened on the network" and "what the system recorded" views of the same event.

---

## Most Valuable Lessons Learned

- **"Normal" traffic is louder than expected.** Capturing on even a small lab network surfaced constant ARP and broadcast chatter — learning to filter that out is its own skill, separate from knowing what to look for.
- **Encryption changes what's visible.** Following an HTTPS stream versus an HTTP stream made concrete why so much of modern security work relies on endpoint and log data rather than packet contents alone — you often can't see inside encrypted payloads.
- **Following a stream beats reading individual packets.** Reconstructing a full request/response conversation gave a much clearer picture of an interaction than looking at isolated frames — this is the difference between reading a sentence and reading individual letters.
- **A completed handshake is a baseline, not a guarantee.** Understanding what "normal" TCP setup looks like made it much easier to reason about what an incomplete or malformed handshake might indicate.

---

## Resources

- [Wireshark User's Guide](https://www.wireshark.org/docs/wsug_html_chunked/)
- [Wireshark Display Filter Reference](https://www.wireshark.org/docs/dfref/)
- [Wireshark Sample Captures (practice files)](https://wiki.wireshark.org/SampleCaptures)
- [TryHackMe: Wireshark Rooms](https://tryhackme.com/room/wiresharktraffic-analysis)
