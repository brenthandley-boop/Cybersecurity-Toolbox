# Wazuh Cheat Sheet
**SIEM & Extended Detection and Response — Quick Reference**

---

## Core Workflow

1. Deploy manager (central server)
2. Install and register agents on monitored endpoints
3. Configure monitored files/directories (FIM) and log sources
4. Tune rules to reduce noise
5. Review alerts in the Wazuh Dashboard, correlate with MITRE ATT&CK where relevant

---

## Agent Commands

| Command | Purpose |
|---|---|
| `WAZUH_MANAGER='<ip>' apt-get install wazuh-agent` | Install agent, pointed at a manager (Debian-based) |
| `systemctl start wazuh-agent` | Start the agent service |
| `systemctl status wazuh-agent` | Check agent status |
| `/var/ossec/bin/agent-auth -m <manager-ip>` | Manually register agent to a manager |
| `/var/ossec/bin/agent-control -l` | List agent connection status (from manager) |

---

## Manager Commands

| Command | Purpose |
|---|---|
| `systemctl status wazuh-manager` | Check manager service status |
| `/var/ossec/bin/wazuh-control status` | Check all Wazuh component statuses |
| `/var/ossec/bin/wazuh-control restart` | Restart all components |

---

## Key File Locations

| Path | Purpose |
|---|---|
| `/var/ossec/etc/ossec.conf` | Main manager configuration file |
| `/var/ossec/etc/rules/` | Custom detection rules |
| `/var/ossec/etc/decoders/` | Custom log decoders |
| `/var/ossec/logs/alerts/alerts.log` | Raw alert log |
| `/var/ossec/logs/ossec.log` | Wazuh's own internal service log (troubleshooting) |

---

## Alert Rule Levels (severity)

| Level | Meaning |
|---|---|
| 0–3 | Low priority / informational |
| 4–7 | Notable — worth review |
| 8–11 | Suspicious activity — attention needed |
| 12–15 | High severity — likely active threat or critical failure |

---

## Common Modules to Know

| Module | Function |
|---|---|
| **File Integrity Monitoring (FIM/syscheck)** | Detects unauthorized file/config changes |
| **Log Data Analysis** | Correlates and analyzes collected logs |
| **Vulnerability Detection** | Matches installed software against known CVEs |
| **Active Response** | Automated actions triggered by alert rules |
| **Security Configuration Assessment (SCA)** | Checks system config against hardening benchmarks (e.g., CIS) |

---

## Pro Tips

- **Default rules generate significant noise** — budget real time for tuning before treating alert volume as meaningful.
- FIM (`syscheck`) requires explicitly configured directories in `ossec.conf` — it doesn't monitor everything by default.
- Cross-reference alert rules against MITRE ATT&CK technique IDs where possible — it turns a raw alert into a framework-mapped finding, which reads much stronger in a report.
- Treat the manager as a high-value asset — anyone with manager access effectively has visibility (and potentially response control) across every connected agent.
- Compare Wazuh's detection logic against a Splunk-based detection pipeline for the same simulated event — useful for understanding SIEM design trade-offs generally, not just this one tool.
