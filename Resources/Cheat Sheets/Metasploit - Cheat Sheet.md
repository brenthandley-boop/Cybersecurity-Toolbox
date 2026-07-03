# Metasploit Cheat Sheet
**Exploitation Framework — Quick Reference**

---

## Core Workflow

1. Confirm authorization + isolated lab/engagement scope
2. Recon target (often via imported Nmap data)
3. Search for a matching module
4. Configure module options (`RHOSTS`, `LHOST`, `PAYLOAD`)
5. Execute and manage the resulting session
6. Post-exploitation, then clean up

---

## Console Basics

| Command | Purpose |
|---|---|
| `msfconsole` | Launch the interactive console |
| `search <term>` | Search modules by keyword |
| `search cve:<CVE-ID>` | Search modules by CVE |
| `use <module path>` | Select a module |
| `info` | Show details on the currently selected module |
| `back` | Deselect current module |

---

## Configuring a Module

| Command | Purpose |
|---|---|
| `show options` | Display required/optional settings |
| `show payloads` | List compatible payloads for the selected exploit |
| `show targets` | List specific target variants (OS/version) |
| `set RHOSTS <ip>` | Set target host(s) |
| `set RPORT <port>` | Set target port |
| `set LHOST <ip>` | Set local (attacker) host for callback |
| `set LPORT <port>` | Set local port for callback |
| `set PAYLOAD <payload>` | Set the payload to deliver |
| `setg <option> <value>` | Set an option globally (persists across module switches) |
| `exploit` / `run` | Execute the module |

---

## Module Types

| Type | Purpose |
|---|---|
| **exploit** | Code that takes advantage of a specific vulnerability |
| **payload** | Code delivered/executed after successful exploitation |
| **auxiliary** | Scanning, fuzzing, DoS — non-exploit utility modules |
| **post** | Post-exploitation actions (privilege escalation, credential harvesting) |
| **encoder** | Obfuscates payloads (e.g., to avoid basic signature detection) |
| **nop** | No-op generators, used in payload construction |

---

## Common Payload
