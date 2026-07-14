# Snort Cheat Sheet
**Network Intrusion Detection / Prevention — Quick Reference**

---

## Core Workflow

1. Validate config (`-T`)
2. Run in passive/sniffer mode to confirm visibility
3. Write or select rules
4. Run as NIDS (alert) mode
5. Tune based on false positives
6. Only move to inline (IPS/blocking) mode once rules are trusted

---

## Modes

| Command | Mode | Purpose |
|---|---|---|
| `snort -v` | Sniffer | Verbose packet headers only |
| `snort -vd` | Sniffer | Headers + packet data |
| `snort -dev -i eth0` | Sniffer | Full packet dump on an interface |
| `snort -l ./log -h 192.168.1.0/24 -c snort.conf` | Packet Logger | Logs traffic for a defined home network |
| `snort -A console -q -c snort.conf -i eth0` | NIDS | Runs detection, alerts printed to console |

---

## Setup & Validation

| Command | Purpose |
|---|---|
| `snort -T -c /etc/snort/snort.conf` | Test/validate a config file without running |
| `snort -V` | Show Snort version |
| `snort -W` | List available network interfaces |

---

## Rule Structure

```
action protocol src_ip src_port -> dst_ip dst_port (options)
```

| Component | Example | Meaning |
|---|---|---|
| **Action** | `alert`, `log`, `pass`, `drop`, `reject` | What to do when the rule matches |
| **Protocol** | `tcp`, `udp`, `icmp`, `ip` | Protocol to inspect |
| **Src/Dst IP & Port** | `any any -> 192.168.1.0/24 80` | Traffic direction and scope |
| **Options** | `(msg:"..."; sid:1000001;)` | Rule metadata and match conditions |

### Common Rule Options

| Option | Purpose |
|---|---|
| `msg:"text"` | Human-readable description shown in the alert |
| `sid:<number>` | Unique rule ID (custom rules should use 1,000,000+) |
| `rev:<number>` | Rule revision number |
| `content:"string"` | Match on a specific string/pattern in the payload |
| `flags:S` | Match TCP flags (e.g., `S` for SYN) |
| `classtype:<type>` | Categorize the rule (e.g., `attempted-recon`) |

### Example Rules

```
# Alert on any HTTP traffic to the home network
alert tcp any any -> 192.168.1.0/24 80 (msg:"HTTP traffic detected"; sid:1000001;)

# Alert on ICMP (potential ping sweep)
alert icmp any any -> 192.168.1.0/24 any (msg:"ICMP traffic detected"; sid:1000002;)

# Alert on a TCP SYN scan pattern
alert tcp any any -> 192.168.1.0/24 any (msg:"Possible SYN scan"; flags:S; sid:1000003;)
```

---

## Alert Actions

| Action | Behavior |
|---|---|
| `alert` | Generate an alert and log the packet |
| `log` | Log the packet, no alert |
| `pass` | Ignore the packet |
| `drop` | Block the packet and log it (inline/IPS mode only) |
| `reject` | Block the packet, log it, and send a rejection response (inline mode only) |

---

## Pro Tips

- **Custom `sid` numbers should start at 1,000,000+** — lower numbers are reserved for official Snort/Talos rules, avoiding collisions.
- **Test every custom rule against known traffic before trusting it** — generate the traffic yourself (e.g., with Scapy or Nmap) and confirm the alert fires as expected.
- **`-T` before every deployment** — a config error silently prevents Snort from starting correctly otherwise.
- **Start broad, then narrow.** A rule that's too broad floods you with noise; too narrow and it misses variations of the same attack.
- **Pair Snort alerts with a Wireshark capture of the same traffic** — seeing both the trigger and the raw packet builds real understanding, not just "the rule fired."
