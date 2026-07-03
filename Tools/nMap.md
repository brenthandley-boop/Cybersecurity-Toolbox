# Nmap - Network Mapper

**Category:** Network Scanning & Discovery  
**Difficulty:** Beginner to Intermediate  
**License:** Open Source (GPL)

## Description

Nmap (**N**etwork **M**apper) is one of the most powerful and widely used open-source tools for network discovery, security auditing, and reconnaissance. It is considered the industry standard for scanning networks to discover hosts, services, open ports, and potential vulnerabilities.

Security professionals use Nmap daily for:
- Asset inventory and network mapping
- Finding open ports and running services
- Operating system and service version detection
- Basic vulnerability scanning
- Penetration testing reconnaissance

## Key Features

- Host discovery
- Port scanning (TCP, UDP, SYN, ACK, etc.)
- Service version detection
- OS fingerprinting
- Nmap Scripting Engine (NSE) — over 600 scripts
- Output in multiple formats (normal, XML, grepable)
- Timing templates for stealth or speed

## Common Commands

### Basic Scans

```bash
# Scan a single IP or hostname
nmap 192.168.1.105
nmap scanme.nmap.org

# Scan a range / subnet
nmap 192.168.1.1-255
nmap 192.168.1.0/24
