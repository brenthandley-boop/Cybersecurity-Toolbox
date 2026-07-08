# Nmap — Network Mapper

**Category:** Network Scanning & Discovery
**Difficulty:** Beginner to Intermediate
**License:** Open Source (GPL)

---

## Description

Nmap (Network Mapper) is one of the most powerful and widely used open-source tools for network discovery, security auditing, and reconnaissance. It is considered the industry standard for scanning networks to discover hosts, services, open ports, and potential vulnerabilities.

Security professionals use Nmap daily for:

- Asset inventory and network mapping
- Finding open ports and running services
- Operating system and service version detection
- Basic vulnerability scanning
- Penetration testing reconnaissance

---

## Key Features

- Host discovery
- Port scanning (TCP, UDP, SYN, ACK, etc.)
- Service version detection
- OS fingerprinting
- Nmap Scripting Engine (NSE) — over 600 scripts
- Output in multiple formats (normal, XML, grepable)
- Timing templates for stealth or speed

---

## Common Commands

### Basic Scans

```bash
# Scan a single IP or hostname
nmap 192.168.1.105
nmap scanme.nmap.org

# Scan a range / subnet
nmap 192.168.1.1-255
nmap 192.168.1.0/24
```

### Port Scanning Techniques

```bash
# TCP SYN scan (default, requires root — fast and relatively stealthy)
nmap -sS 192.168.1.105

# TCP Connect scan (no root required, more detectable)
nmap -sT 192.168.1.105

# UDP scan
nmap -sU 192.168.1.105

# Scan specific ports
nmap -p 22,80,443 192.168.1.105
nmap -p 1-1000 192.168.1.105
```

### Service & OS Detection

```bash
# Service/version detection
nmap -sV 192.168.1.105

# OS fingerprinting
nmap -O 192.168.1.105

# Aggressive scan (OS detection + version detection + script scanning + traceroute)
nmap -A 192.168.1.105
```

### Nmap Scripting Engine (NSE)

```bash
# Run default safe scripts
nmap -sC 192.168.1.105

# Run a specific vulnerability-detection script
nmap --script http-vuln-cve2017-5638 192.168.1.105
```

### Output & Timing

```bash
# Save output in multiple formats
nmap -A -oN scan.txt -oX scan.xml 192.168.1.0/24

# Timing templates (T0 = paranoid/slow, T5 = insane/fast)
nmap -T4 192.168.1.0/24
```

---

## Hands-On Learning Path

Nmap proficiency is built by scanning progressively more realistic targets — on infrastructure that's explicitly legal to test. Below is the progression most cybersecurity students and self-taught practitioners use to build reps. Checked items reflect scans actually completed in my own lab or against authorized public targets.

**Public, legal-to-scan targets**
- [x] `scanme.nmap.org` — Nmap's own official test target, safe for basic scan practice
- [ ] TryHackMe "Nmap" and "Nmap: The Basics" rooms — guided, scored scanning exercises
- [ ] OverTheWire "Bandit" wargame — light recon practice as part of a broader CTF-style challenge

**Home lab (VirtualBox / isolated network)**
- [x] Basic host discovery scan across a private subnet (`192.168.1.0/24`)
- [x] Service and version enumeration against a Metasploitable2 VM
- [x] Aggressive scan (`-A`) combining OS detection, version detection, NSE, and traceroute
- [ ] Comparing SYN scan vs. Connect scan output/timing on the same target
- [ ] Writing a custom NSE-driven scan against a deliberately outdated service to confirm a known CVE

**Applied / integration practice**
- [ ] Feeding Nmap XML output (`-oX`) into a parsing script to automate reporting
- [ ] Cross-referencing an Nmap scan against Wireshark capture of the same scan, to see both sides of the traffic

---

## Hands-on Walkthrough Examples
#### Example 1: Basic Network Discovery
- Scanned my home lab network (10.0.2.0/24) to identify live hosts and services.
 <img width="987" height="984" alt="Screenshot 2026-07-07 140317" src="https://github.com/user-attachments/assets/62e27ab9-3843-4db2-a7e7-6a8ff3686deb" />

#### Example 2: Detailed Service Enumeration
- Scanned a vulnerable Metasploitable 2 VM with version detection and scripting.
 <img width="984" height="884" alt="Screenshot 2026-07-08 121330" src="https://github.com/user-attachments/assets/4f1afe91-77ce-457b-937f-2736596e141c" />

#### Example 3: Aggressive Scan
- Used nmap -A to gather OS, services, and traceroute information.
 <img width="1226" height="854" alt="Screenshot 2026-07-08 122851" src="https://github.com/user-attachments/assets/5bd1091d-c700-4c99-8dec-efc86282f78d" />

 ---

## Best Practices

- **Get explicit authorization first.** Never scan a network or host you don't own or don't have written permission to test — unauthorized scanning can violate policy or law even when no harm is intended.
- **Match the scan to the goal.** Use lighter, targeted scans (`-sV` on specific ports) when you know what you're looking for; reserve `-A` and full-range scans for situations where broad discovery is actually needed.
- **Consider timing and noise.** Faster timing templates (`-T4`/`-T5`) increase detection risk and can affect network performance — default to a more conservative template on production or shared networks.
- **Always log your output.** Save scans in multiple formats (`-oN`, `-oX`) so results can be reviewed, diffed against future scans, or fed into other tools.
- **Verify findings before acting on them.** Nmap's OS/version detection is a best-guess based on fingerprinting — confirm anything critical before making a security decision based on it.

---

## Most Valuable Lessons Learned

- **The scan type is a decision, not a default.** Choosing `-sS` vs `-sT`, or a narrow port range vs. a full sweep, forces you to think about what you're actually trying to learn — that's a more useful habit than memorizing flags.
- **Timing has real trade-offs.** Running the same scan at different `-T` levels made it clear why "just use `-T5` for speed" is bad advice outside of a lab — it's the loudest, most detectable option.
- **NSE turns Nmap into more than a mapper.** Scripts like `http-vuln-cve2017-5638` showed me that a single scan can move from "here's what's open" to "here's a specific, known vulnerability" — which is a meaningfully different kind of finding.
- **Aggressive scanning is a liability outside a controlled environment.** Running `-A` made the noise and detection risk obvious firsthand — reinforcing why scope and authorization aren't just policy checkboxes, they're operational necessities.

---

## Resources

- [Official Nmap Documentation](https://nmap.org/book/man.html)
- [Nmap Scripting Engine (NSE) Library](https://nmap.org/nsedoc/)
- [Nmap Network Scanning (the official book, Gordon Lyon)](https://nmap.org/book/toc.html)
- [TryHackMe: Nmap Room](https://tryhackme.com/room/furthernmap)
