# Wireshark - Network Protocol Analyzer

**Category:** Packet Capture & Analysis  
**Difficulty:** Beginner to Intermediate  

## Description

Wireshark is the world’s most popular network protocol analyzer. It allows you to capture and interactively browse traffic running on a computer network in real time.

## Key Features
- Deep inspection of hundreds of protocols
- Powerful display filters
- Live packet capture and offline analysis
- VoIP analysis, decryption support (SSL/TLS with key)
- Rich visualization (IO graphs, conversations, endpoints)

## Common Filters & Commands

```bash
# Capture filter examples (applied during capture)
tcp port 80 or tcp port 443
host 192.168.1.105
not arp and not icmp

# Display filter examples (applied after capture)
http
dns
tcp.port == 443
http.request.method == "POST"
frame contains "password"
