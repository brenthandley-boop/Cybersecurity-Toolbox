# Nikto — Web Server Scanner

**Category:** Web Server Vulnerability Scanning
**Difficulty:** Beginner
**License:** Open Source (GPL)

---

## Description

Nikto is a fast, open-source command-line scanner that checks web servers against thousands of known issues — outdated software versions, dangerous files and CGIs, and common misconfigurations. It's typically the first tool run against a web server, giving a broad "what's obviously wrong here" pass before deeper manual testing with tools like Burp Suite or OWASP ZAP.

Security professionals use Nikto daily for:

- Quick misconfiguration and outdated-software checks at the start of an assessment
- Establishing an initial risk baseline before investing time in manual testing
- Identifying dangerous or forgotten files/CGIs left exposed on a web server
- Validating that basic server hardening (headers, banners, default files) has actually been done

---

## Key Features

- 6,700+ checks for dangerous files, CGIs, and known vulnerabilities
- Outdated server software/version detection
- SSL/TLS support
- Tunable test categories (`-Tuning`) to scope a scan to specific check types
- Multiple output formats (txt, HTML, XML, CSV)
- Proxy support — can route scans through Burp Suite for deeper inspection of the traffic it generates

---

## Common Commands

### Basic Scans

```bash
# Basic scan against a host
nikto -h example.com

# Scan specific ports
nikto -h example.com -p 80,443

# Scan over SSL/TLS
nikto -h https://example.com -ssl
```

### Scoping and Tuning

```bash
# Limit scan to specific test categories (e.g., 1=file retrieval, 2=misconfig)
nikto -h example.com -Tuning 1,2,3
```

### Output and Integration

```bash
# Save output to a formatted report
nikto -h example.com -o report.html -Format html

# Route scan traffic through Burp Suite for inspection
nikto -h example.com -useproxy http://127.0.0.1:8080
```

---

## Hands-On Learning Path

Nikto proficiency comes from learning to separate real findings from the noise it generates — the tool is intentionally broad, not precise. Below is the progression most cybersecurity students use to build reps.

**Guided / official starting points**
- [ ] TryHackMe "Nikto" room
- [ ] Running a scan against OWASP Juice Shop as a first-pass reconnaissance step

**Home lab (VirtualBox / isolated network)**
- [ ] Scanning DVWA at different security levels and comparing what Nikto flags at each
- [ ] Routing a Nikto scan through Burp Suite's proxy to see the full request/response traffic it generates
- [ ] Comparing Nikto's automated findings against manual testing of the same target with Burp or ZAP

**Applied / integration practice**
- [ ] Using Nikto as the first step in a layered workflow: Nikto → manual verification → deeper testing with Burp/ZAP
- [ ] Documenting which Nikto findings were true positives vs. false positives after manual review

---

## Best Practices

- **Get explicit authorization first.** Nikto is loud and easily logged — running it against a target without permission is a fast way to trip alarms and violate policy.
- **Treat it as a first pass, not a final report.** Nikto favors breadth over precision; verify findings manually before including them anywhere official.
- **Expect false positives.** Version banners and generic checks routinely misfire — confirm before flagging a finding as real.
- **Watch server load and stability.** Older or fragile web servers can be destabilized by a full scan — throttle timing or schedule accordingly.
- **Never run against production without a change window and documented permission.**

---

## Most Valuable Lessons Learned *(in progress)*

This section will grow with real findings as labs above are completed. Early conceptual takeaway:

- **Breadth and precision are different goals.** Nikto's value is in surfacing a wide net of possibilities quickly — the actual skill is in the manual triage afterward, not the scan itself.

I'd rather keep this honest and incremental than pad it — real scan comparisons and findings will replace this note as work is completed.

---

## Resources

- [Nikto GitHub Repository](https://github.com/sullo/nikto)
- [TryHackMe: Nikto Room](https://tryhackme.com/room/nikto)
- [OWASP Juice Shop (practice target)](https://owasp.org/www-project-juice-shop/)
