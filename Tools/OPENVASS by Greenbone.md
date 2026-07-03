# OpenVAS (Greenbone) — Vulnerability Scanning

**Category:** Vulnerability Scanning & Management
**Difficulty:** Intermediate
**License:** Open Source (Greenbone Community Edition) / Paid Enterprise tiers available

---

## Description

OpenVAS, now the scan engine behind Greenbone Vulnerability Management, is a full-featured vulnerability scanner that checks hosts against a continuously updated feed of known CVEs (Network Vulnerability Tests, or NVTs). It's a free, open-source alternative to commercial scanners like Nessus or Qualys, and supports both unauthenticated and authenticated (credentialed) scanning.

Security professionals use OpenVAS daily for:

- Enterprise-scale vulnerability assessments across large host inventories
- Patch-prioritization support via CVSS-based severity scoring
- Recurring, scheduled scanning as part of a vulnerability management program
- Compliance-driven scanning requirements

---

## Key Features

- Continuously updated NVT feed for current CVE coverage
- Authenticated (credentialed) and unauthenticated scanning
- Web-based GUI (Greenbone Security Assistant) for scan management
- CVSS-based severity scoring for prioritization
- Scheduled/recurring scans
- Report export (PDF, XML, CSV)

---

## Common Commands

OpenVAS is primarily GUI-driven; CLI/API access is available via `gvm-cli`.

```bash
# Initial setup and service management
gvm-setup
gvm-start
gvm-check-setup
```

```
Typical scan workflow (via GUI):
1. Configure a Target (host/IP range, optional credentials)
2. Create a Task (target + scan config)
3. Run the Task
4. Review the Report, sorted by CVSS severity
```

---

## Hands-On Learning Path

OpenVAS proficiency comes from running real scans against known-vulnerable targets and learning to read a full report critically, not just running the default configuration. Below is the progression most cybersecurity students use to build reps.

**Guided / official starting points**
- [ ] Installing Greenbone Community Edition following the official setup docs
- [ ] Reviewing a sample scan report to understand CVSS scoring and severity breakdowns before running a first real scan

**Home lab (VirtualBox / isolated network)**
- [ ] Running an unauthenticated scan against a Metasploitable2 VM
- [ ] Running the same scan authenticated, to directly compare depth of findings
- [ ] Cross-referencing OpenVAS's CVE findings against vulnerabilities manually confirmed via Nmap NSE scripts

**Applied / integration practice**
- [ ] Practicing full report triage — sorting and prioritizing findings by CVSS score and exploitability
- [ ] Scheduling a recurring scan and comparing results across two scan cycles to see how findings change after a simulated patch

---

## Best Practices

- **Get explicit authorization first**, especially for authenticated scans, which require credentials with real system access.
- **Prefer authenticated scans when possible.** Unauthenticated scans have real blind spots and can significantly understate actual risk.
- **Keep the NVT feed updated.** An outdated feed means missing recently disclosed CVEs entirely.
- **Schedule scans deliberately.** Full scans are resource-intensive and can affect target performance — avoid production during business hours without a change window.
- **Triage before reporting.** Not every finding is exploitable in context — validate before it goes into a report or ticket.
- **Protect scan credentials.** Authenticated scanning requires storing real system credentials — treat that credential store as a high-value target itself.

---

## Most Valuable Lessons Learned *(in progress)*

This section will grow with real findings as labs above are completed. Early conceptual takeaway:

- **Authenticated vs. unauthenticated is the real dividing line.** Understanding how much risk an unauthenticated scan can miss reframed how I think about "we run vulnerability scans" as a claim — the type of scan matters as much as the fact that one runs at all.

I'd rather keep this honest and incremental than pad it — real scan comparisons and findings will replace this note as work is completed.

---

## Resources

- [Greenbone Community Documentation](https://greenbone.github.io/docs/)
- [OpenVAS / GVM GitHub Repository](https://github.com/greenbone)
- [CVSS Scoring Guide (FIRST.org)](https://www.first.org/cvss/)
