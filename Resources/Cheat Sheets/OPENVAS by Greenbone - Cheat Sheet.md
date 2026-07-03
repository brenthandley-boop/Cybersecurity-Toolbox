# OpenVAS (Greenbone) Cheat Sheet
**Vulnerability Scanning & Management — Quick Reference**

---

## Core Workflow

1. Configure a **Target** (host/IP range, optional credentials for authenticated scanning)
2. Select a **Scan Config** (defines which NVTs run)
3. Create and run a **Task** (target + config)
4. Review the **Report**, sorted by CVSS severity
5. Triage findings — confirm before escalating to remediation

---

## Setup / Service Commands

| Command | Purpose |
|---|---|
| `gvm-setup` | Initial installation/configuration |
| `gvm-check-setup` | Verify setup completed correctly |
| `gvm-start` | Start all GVM/OpenVAS services |
| `gvm-stop` | Stop all services |
| `gvm-feed-update` | Manually refresh the NVT/CVE feed |

---

## Scan Configs (built-in, common)

| Config | Behavior |
|---|---|
| **Full and fast** | Default — broad coverage, reasonably efficient |
| **Full and fast ultimate** | Includes checks that may disrupt the target (DoS-risk NVTs) — use with caution |
| **Discovery** | Host/service discovery only, no vulnerability checks |
| **Host Discovery** | Lightweight — just confirms which hosts are alive |
| **System Discovery** | OS and service fingerprinting, minimal vuln checks |

---

## Severity / CVSS Reference

| CVSS Score | Severity |
|---|---|
| 9.0 – 10.0 | Critical |
| 7.0 – 8.9 | High |
| 4.0 – 6.9 | Medium |
| 0.1 – 3.9 | Low |
| 0.0 | None/Informational |

---

## Authenticated vs. Unauthenticated

| Scan Type | Visibility | Notes |
|---|---|---|
| **Unauthenticated** | External/network-visible issues only | Faster, no credential risk, but significant blind spots |
| **Authenticated** | Full local software/patch inventory | Requires storing credentials securely; much more accurate |

---

## Pro Tips

- **Authenticated scans reveal dramatically more** — an unauthenticated scan alone can create false confidence in a system's patch state.
- Schedule full/"ultimate" configs only in maintenance windows — some NVTs can genuinely disrupt fragile services.
- Keep the feed updated (`gvm-feed-update`) before any scan you intend to report on — stale feeds miss recent CVEs.
- Export reports in multiple formats (PDF for stakeholders, XML/CSV for further processing or ticketing integration).
- Treat every "High/Critical" finding as a starting point for manual verification, not an automatic ticket — false positives happen.
