# Wireshark Cheat Sheet
**Network Protocol Analysis — Quick Reference**

---

## Core Workflow

1. Select capture interface
2. Apply a **capture filter** (optional — limits what's recorded)
3. Capture traffic
4. Apply **display filters** to narrow the view
5. Follow a stream to reconstruct a full conversation
6. Export objects / save filtered results for reporting

---

## Capture Filters (set before capture)

*(Uses BPF syntax — different from display filter syntax below)*

| Filter | Result |
|---|---|
| `host 192.168.1.5` | Traffic to/from a specific host |
| `net 192.168.1.0/24` | Traffic within a subnet |
| `port 80` | Traffic on a specific port |
| `tcp port 443` | TCP traffic on a specific port |
| `not arp and not dns` | Exclude common background noise |

---

## Display Filters (applied after capture)

| Filter | Result |
|---|---|
| `ip.addr == 192.168.1.5` | Traffic to/from an IP |
| `tcp.port == 443` | TCP traffic on a port |
| `http.request` | HTTP requests only |
| `http.response.code == 200` | Successful HTTP responses |
| `dns.flags.response == 0` | DNS queries (not responses) |
| `tcp.flags.syn==1 && tcp.flags.ack==0` | SYN packets (connection attempts) |
| `tcp.analysis.retransmission` | Retransmitted packets (possible network issue) |
| `tls.handshake.type == 1` | TLS Client Hello |
| `arp` | ARP traffic |
| `frame contains "password"` | Payload search (cleartext protocols only) |

**Combine filters:** `&&` (and), `||` (or), `!` (not)

---

## Following Conversations

| Action | How |
|---|---|
| Follow TCP Stream | Right-click packet → Follow → TCP Stream |
| Follow HTTP Stream | Right-click packet → Follow → HTTP Stream |
| Follow UDP Stream | Right-click packet → Follow → UDP Stream |
| View conversation stats | Statistics → Conversations |
| Protocol breakdown | Statistics → Protocol Hierarchy |

---

## Useful Keyboard Shortcuts

| Shortcut | Action |
|---|---|
| `Ctrl+E` | Start/stop capture |
| `Ctrl+F` | Find packet |
| `Ctrl+→ / Ctrl+←` | Jump between marked packets |
| `Ctrl+M` | Mark/unmark a packet |
| `Ctrl+Alt+Shift+T` | Apply as filter (from selected field) |

---

## tshark (CLI) Quick Reference

| Command | Result |
|---|---|
| `tshark -D` | List available interfaces |
| `tshark -i eth0 -c 100` | Capture 100 packets on eth0 |
| `tshark -i eth0 -w cap.pcapng` | Capture and save to file |
| `tshark -r cap.pcapng -Y "http.request"` | Read file, apply display filter |
| `tshark -r cap.pcapng -T fields -e ip.src -e ip.dst` | Extract specific fields for scripting |

---

## Pro Tips

- **Capture filters reduce file size; display filters organize analysis** — don't confuse the two syntaxes (they're genuinely different grammars).
- Color rules (View → Coloring Rules) can visually flag retransmissions, errors, or specific hosts at a glance.
- `Statistics → I/O Graph` is the fastest way to spot a traffic spike (e.g., DoS, large exfil) in a big capture.
- Encrypted traffic (HTTPS/TLS) hides payload content — pair Wireshark with endpoint/log data for anything beyond metadata analysis.
- Export credentials/objects only in authorized lab environments — this is genuinely sensitive capability.
