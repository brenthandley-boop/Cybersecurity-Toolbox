# 🛡️ Cybersecurity Toolbox

**A hands-on portfolio of core cybersecurity tools — how they work, why they matter, and how I use them.**

> Built by someone who spent 7+ years in client-facing SaaS and account management before retraining as a cybersecurity analyst — I bring technical depth *and* the communication skills to explain risk to people who aren't in the weeds with me.

---

## 👋 About This Repo

This is a living toolbox, not a tutorial dump. Each tool folder follows the same format:

- **What it is and why it matters** in a real SOC/security workflow
- **Core commands and functionality** I understand deeply — not just a surface-level list
- **A hands-on learning path** — the concrete labs and exercises used to build real proficiency, checked off as completed
- **Best practices and lessons learned** from actually using the tool, not just reading about it

Every tool also has a companion entry in **[`cheatsheets/`](./cheatsheets/)** — a dense, table-driven quick reference for exact flags, syntax, and commands, meant to be pulled up mid-task rather than read start to finish.

The goal isn't to show that I've *heard of* these tools. It's to show how I think when I'm using them.

---

## 🎯 Who I Am

- Fullstack Academy Cybersecurity Analytics graduate (2026)
- Background in account management, client relations, and SaaS sales (NBCUniversal, Riverway Ventures) — I know how to communicate technical risk to non-technical stakeholders
- Studying for CompTIA Security+ (SY0-701)
- Based in NYC — targeting SOC Analyst and Cybersecurity Awareness Specialist roles
- [LinkedIn](#) · [Resume](#) · [Email](#)

---

## 🧰 Tools Covered

| Tool | Category | Focus |
|---|---|---|
| [Nmap](./01-nmap/) | Network Reconnaissance | Host discovery, port scanning, service/version enumeration |
| [Wireshark](./02-wireshark/) | Traffic Analysis | Packet capture, protocol inspection, anomaly detection |
| [Burp Suite](./03-burpsuite/) | Web Application Security | Intercepting proxy, manual testing, vulnerability discovery |
| [John the Ripper](./04-johntheripper/) | Password Security | Hash cracking, credential/password-strength auditing |
| [theHarvester](./05-theharvester/) | OSINT & Reconnaissance | Email/subdomain/employee discovery from public sources |
| [OWASP ZAP](./06-owaspzap/) | Web Application Security | Automated scanning, intercepting proxy, CI/CD integration |
| [Nikto](./07-nikto/) | Web Server Scanning | Fast misconfiguration and outdated-software checks |
| [OpenVAS (Greenbone)](./08-openvas/) | Vulnerability Management | Authenticated/unauthenticated CVE scanning at scale |
| [sqlmap](./09-sqlmap/) | Web Application Security | Automated SQL injection detection and exploitation |
| [Wazuh](./10-wazuh/) | SIEM / XDR | Log correlation, file integrity monitoring, detection engineering |
| [Autopsy](./11-autopsy/) | Digital Forensics & Incident Response | Disk image analysis, file recovery, timeline reconstruction |
| [Metasploit](./12-metasploit/) | Exploitation Framework | Exploit validation, payload delivery, post-exploitation |

> 📌 A separate detection-engineering capstone (Splunk + Hydra + MITRE ATT&CK mapping) lives in its own repo: **[soc-detection-lab →](#)**

---

## 📋 Quick-Reference Cheat Sheets

Fast, table-driven syntax lookups for every tool above — flags, filters, common commands, and pro tips in one scannable page each.

| Cheat Sheet | | Cheat Sheet |
|---|---|---|
| [Nmap](./cheatsheets/nmap-cheatsheet.md) | | [Nikto](./cheatsheets/nikto-cheatsheet.md) |
| [Wireshark](./cheatsheets/wireshark-cheatsheet.md) | | [OpenVAS](./cheatsheets/openvas-cheatsheet.md) |
| [Burp Suite](./cheatsheets/burpsuite-cheatsheet.md) | | [sqlmap](./cheatsheets/sqlmap-cheatsheet.md) |
| [John the Ripper](./cheatsheets/johntheripper-cheatsheet.md) | | [Wazuh](./cheatsheets/wazuh-cheatsheet.md) |
| [theHarvester](./cheatsheets/theharvester-cheatsheet.md) | | [OWASP ZAP](./cheatsheets/owaspzap-cheatsheet.md) |
| [Autopsy](./cheatsheets/autopsy-cheatsheet.md) | | [Metasploit](./cheatsheets/metasploit-cheatsheet.md) |

---

## 🗂️ Repo Structure

```
cybersecurity-toolbox/
├── README.md
├── 01-nmap/
│   └── README.md
├── 02-wireshark/
│   └── README.md
├── 03-burpsuite/
│   └── README.md
├── 04-johntheripper/
│   └── README.md
├── 05-theharvester/
│   └── README.md
├── 06-owaspzap/
│   └── README.md
├── 07-nikto/
│   └── README.md
├── 08-openvas/
│   └── README.md
├── 09-sqlmap/
│   └── README.md
├── 10-wazuh/
│   └── README.md
├── 11-autopsy/
│   └── README.md
├── 12-metasploit/
│   └── README.md
└── cheatsheets/
    ├── nmap-cheatsheet.md
    ├── wireshark-cheatsheet.md
    ├── burpsuite-cheatsheet.md
    ├── johntheripper-cheatsheet.md
    ├── theharvester-cheatsheet.md
    ├── owaspzap-cheatsheet.md
    ├── nikto-cheatsheet.md
    ├── openvas-cheatsheet.md
    ├── sqlmap-cheatsheet.md
    ├── wazuh-cheatsheet.md
    ├── autopsy-cheatsheet.md
    └── metasploit-cheatsheet.md
```

Every tool folder is self-contained — click in and you'll get the full picture without needing context from elsewhere in the repo.

---

## 🧭 How to Navigate

- **Short on time?** Read any tool's `README.md` — that's the full summary in one page.
- **Want exact syntax fast?** Check the matching file in `cheatsheets/` — no narrative, just tables.
- **Want proof of real hands-on work?** Look for checked (`✅`) items in each tool's Hands-On Learning Path — unchecked items are the honest, visible roadmap of what's still in progress.

---

## 📌 Status

This repo is actively maintained as I continue building lab reps and studying for Security+. Star or check back for updates.# Cybersecurity-Toolbox - Practical Walk-thru
A working cybersecurity tool box equiped to ensure the capacity to hit the ground running from day one. This includes the essentials collection of free and open-source cybersecurity tools with hands-on walkthroughs, command references, and real lab examples covering network security, reconnaissance, web application testing, forensics, and more. 

##Why This Repository Exists
While studying for CompTIA Security+, I realized that knowing about tools is different from knowing how to use them. This repo serves as my personal reference guide and a living portfolio piece to show employers my practical experience.

All tools were tested in an isolated VirtualBox lab environment (Kali Linux + vulnerable VMs).

## How to Use This Repo
Browse the tools/ folder for detailed walkthroughs
Check the screenshots/ folder for visual examples
Feel free to use any commands or notes in your own lab (ethically!)

## Lab Environment Used
**Host**: Windows 11
**Hypervisor**: VirtualBox
**Attack VM**: Kali Linux 2025
**Target VMs** Metasploitable 2, DVWA, Juice Shop

Future Additions
Ghidra, Volatility 3, Snort, Fail2Ban, YARA, etc.

---

Last Updated: July 2026
Author: Brent Handley

⭐ Star this repo if you find it helpful!
Status: Actively Maintained
