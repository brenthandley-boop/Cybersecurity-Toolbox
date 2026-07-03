# Nmap Cheat Sheet
**Network Scanning & Discovery — Quick Reference**

---

## Core Workflow

1. Host discovery (is it alive?)
2. Port scan (what's open?)
3. Service/version detection (what's running?)
4. NSE scripts (any known issues?)
5. Save output for reporting

---

## Scan Types

| Flag | Scan Type | Notes |
|---|---|---|
| `-sS` | TCP SYN scan | Default for privileged users; fast, half-open, relatively stealthy |
| `-sT` | TCP Connect scan | Full handshake; used when raw sockets unavailable (no root) |
| `-sU` | UDP scan | Slower; many services silently drop UDP probes |
| `-sA` | ACK scan | Firewall rule mapping, not open-port detection |
| `-sN` / `-sF` / `-sX` | Null / FIN / Xmas scans | Firewall/IDS evasion; unreliable against modern stacks |
| `-Pn` | Skip host discovery | Treats all hosts as online (useful when ICMP is blocked) |

---

## Host & Port Targeting

| Command | Result |
|---|---|
| `nmap 192.168.1.1` | Single host |
| `nmap 192.168.1.1-50` | Range |
| `nmap 192.168.1.0/24` | Full subnet (CIDR) |
| `nmap -iL targets.txt` | Scan list of hosts from file |
| `nmap -p 80` | Single port |
| `nmap -p 22,80,443` | Specific ports |
| `nmap -p 1-1000` | Port range |
| `nmap -p-` | All 65535 ports |
| `nmap -F` | Fast scan (top 100 ports) |
| `nmap --top-ports 20` | Top N most common ports |

---

## Detection Flags

| Flag | Purpose |
|---|---|
| `-sV` | Service/version detection |
| `-O` | OS fingerprinting |
| `-A` | Aggressive: OS + version + scripts + traceroute |
| `--version-intensity <0-9>` | Tune version-detection depth vs. speed |

---

## Timing Templates

| Flag | Name | Use Case |
|---|---|---|
| `-T0` | Paranoid | IDS evasion, extremely slow |
| `-T1` | Sneaky | IDS evasion |
| `-T2` | Polite | Reduces bandwidth/target load |
| `-T3` | Normal | Default |
| `-T4` | Aggressive | Fast, assumes reliable network — most common lab choice |
| `-T5` | Insane | Fastest, sacrifices accuracy, very noisy |

---

## NSE (Scripting Engine)

| Command | Purpose |
|---|---|
| `-sC` | Run default safe scripts |
| `--script vuln` | Run all vulnerability-detection scripts in category |
| `--script <name>` | Run a specific script |
| `--script-args <args>` | Pass arguments to a script |
| `ls /usr/share/nmap/scripts/` | List installed NSE scripts locally |

**Common categories:** `auth`, `default`, `discovery`, `exploit`, `intrusive`, `malware`, `safe`, `vuln`

---

## Output Formats

| Flag | Format | Use Case |
|---|---|---|
| `-oN file.txt` | Normal | Human-readable |
| `-oX file.xml` | XML | Parsing/automation |
| `-oG file.gnmap` | Grepable | Quick `grep`/`awk` filtering |
| `-oA basename` | All formats | Saves `.nmap`, `.xml`, `.gnmap` at once |

---

## Pro Tips

- `-Pn` is essential when scanning hosts that block ICMP (common on hardened targets).
- Combine `-oA` with every scan you run in a lab — you'll want the XML later even if you don't think so now.
- `--reason` shows *why* Nmap made a given determination (useful for learning, not just results).
- Firewalls/IDS often key on `-sS` + `-T4/T5` combos — if practicing evasion concepts, vary timing and scan type together.
- `nmap --script-help <script>` shows a script's purpose and arguments before you run it blind.
