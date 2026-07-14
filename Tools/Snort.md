# Snort — Network Intrusion Detection & Prevention

**Category:** Network Intrusion Detection / Prevention (NIDS/NIPS)
**Difficulty:** Intermediate
**License:** Open Source (GPL) — maintained by Cisco

---

## Description

Snort is an open-source network intrusion detection and prevention system that analyzes traffic in real time against a customizable rule set to flag malicious activity, policy violations, and known attack signatures. It's one of the most widely deployed open-source IDS engines, and the rule-writing skills it teaches carry directly into commercial NIDS/NIPS platforms.

Security professionals use Snort daily for:

- Real-time network traffic monitoring and alerting
- Signature-based detection of known attack patterns
- Writing custom detection rules tailored to a specific environment
- Complementing host/log-based tools (like Wazuh) with network-layer visibility

---

## Key Features

- Three operating modes: sniffer, packet logger, and full NIDS/NIPS
- Custom rule-writing language for defining exactly what to detect
- Preprocessors for protocol anomaly detection (e.g., malformed packets)
- Community and registered (Cisco Talos) rule sets, regularly updated
- Can run passively (IDS — alert only) or inline (IPS — actively block)
- Flexible logging output (console, syslog, unified2, database)

---

## Common Commands

### Modes

```bash
# Sniffer mode — verbose packet output
snort -v

# Sniffer mode with packet data shown
snort -vd

# Full packet dump on a specific interface
snort -dev -i eth0
```

### Running as NIDS

```bash
# Run with a config file, log to a directory, alert to console
snort -A console -q -c /etc/snort/snort.conf -i eth0

# Log traffic for a defined home network
snort -l ./log -h 192.168.1.0/24 -c snort.conf
```

### Configuration Testing

```bash
# Validate a config file without actually running
snort -T -c /etc/snort/snort.conf
```

### Basic Rule Syntax

```
alert tcp any any -> 192.168.1.0/24 80 (msg:"HTTP traffic detected"; sid:1000001;)
```

---

## Hands-On Learning Path

Snort proficiency comes from writing and testing your own rules against real traffic — not just running the default rule set. Below is the progression most cybersecurity students use to build reps.

**Guided / official starting points**
- [ ] Snort's official Getting Started documentation
- [ ] TryHackMe "Snort" and "Snort Challenge" rooms

**Home lab (VirtualBox / isolated network)**
- [ ] Running Snort in sniffer mode to confirm basic traffic visibility
- [ ] Writing a custom rule to detect a specific pattern (e.g., an ICMP ping sweep) and confirming it fires correctly
- [ ] Running an Nmap scan against a lab target while Snort is active, to see which default rules trigger

**Applied / integration practice**
- [ ] Comparing a Snort alert against the same traffic captured in Wireshark, to fully understand what triggered the rule at the packet level
- [ ] Feeding Snort alerts into a SIEM (e.g., Wazuh) for centralized correlation
- [ ] Mapping custom rules to relevant MITRE ATT&CK techniques, consistent with the framework used throughout the rest of this portfolio

---

## Best Practices

- **Get explicit authorization, especially for inline (IPS) mode.** Active blocking can disrupt legitimate traffic if a rule is miscalibrated.
- **Start in passive IDS mode before enabling inline blocking.** Confirm rule accuracy before giving Snort the ability to drop traffic.
- **Tune rules to reduce false positives.** An unmanaged ruleset — especially with community rules enabled broadly — generates significant noise.
- **Keep the ruleset updated.** Cisco Talos and community rule feeds are only useful if refreshed regularly.
- **Understand preprocessors before enabling all of them.** Some carry real performance costs — enable deliberately, not by default.
- **Document custom rules clearly**, including a consistent `sid` numbering scheme and descriptive `msg` fields — someone else should be able to understand a rule's intent at a glance.

---

## Most Valuable Lessons Learned *(in progress)*

This section will grow with real findings as labs above are completed. Early conceptual takeaway:

- **Writing a rule that fires is easy — writing one that fires *correctly* is the actual skill.** A rule with a poorly scoped condition can flag legitimate traffic just as easily as it flags something malicious.

I'd rather keep this honest and incremental than pad it — real rule-writing notes and alert findings will replace this note as work is completed.

---

## Resources

- [Snort Official Documentation](https://www.snort.org/documents)
- [Snort Community Rules](https://www.snort.org/downloads/#rule-downloads)
- [Cisco Talos Intelligence Group](https://talosintelligence.com/)
- [TryHackMe: Snort Rooms](https://tryhackme.com/room/snort)
