
# OWASP ZAP — Web Application Security Scanner

**Category:** Web Application Security
**Difficulty:** Beginner to Intermediate
**License:** Open Source (Apache 2.0)

---

## Description

OWASP ZAP (Zed Attack Proxy) is a free, open-source web application security scanner maintained by the OWASP Foundation. Like Burp Suite, it works as an intercepting proxy between browser and target application — but ZAP places heavier emphasis on automated scanning and is fully open-source, making it a common starting point for students and a staple in CI/CD security pipelines.

Security professionals use OWASP ZAP daily for:

- Automated baseline security scans of web applications
- Manual testing via its intercepting proxy, similar to Burp Suite's core workflow
- Integrating security scanning directly into CI/CD pipelines
- Learning web application vulnerability classes in a free, fully-featured tool

---

## Key Features

- Intercepting proxy for manual request/response inspection and modification
- Automated Spider (crawler) to map an application's structure
- Passive scanning (analyzes traffic without sending attack payloads)
- Active scanning (sends attack payloads to test for vulnerabilities — can affect application state)
- Fuzzer for testing input fields with varied payloads
- Automation Framework and CLI (`zap-cli`, Docker images) for scripted/CI-CD use
- HUD (Heads-Up Display) — overlays ZAP's findings directly onto the browser during manual testing

---

## Common Commands

### Docker Quick-Start (Baseline Scan)

```bash
# Run a passive baseline scan against a target
docker run -t owasp/zap2docker-stable zap-baseline.py -t https://example.com
```

### Using zap-cli

```bash
# Start ZAP daemon
zap-cli start

# Spider a target to map its structure
zap-cli spider https://example.com

# Run an active scan (only against authorized targets)
zap-cli active-scan https://example.com

# Generate an HTML report of findings
zap-cli report -o report.html -f html
```

### Full Automated Scan (Docker)

```bash
# Passive + active scan combined, with a generated report
docker run -t owasp/zap2docker-stable zap-full-scan.py -t https://example.com -r report.html
```

---

## Hands-On Learning Path

ZAP proficiency is built by scanning intentionally vulnerable applications before touching anything with real stakes. Below is the progression most cybersecurity students and self-taught practitioners use to build reps.

**Guided / official starting points**
- [ ] OWASP's official "Zap in Ten" video tutorial series
- [ ] Running a baseline scan against OWASP Juice Shop
- [ ] TryHackMe "OWASP ZAP" room

**Home lab (VirtualBox / isolated network)**
- [ ] Running a full active scan against DVWA at increasing security levels, and comparing findings
- [ ] Using the intercepting proxy manually to modify a request, mirroring the Burp Suite Repeater workflow
- [ ] Comparing ZAP's automated findings against manual testing of the same application, to see what automation catches and misses

**Applied / integration practice**
- [ ] Setting up a ZAP baseline scan as a step in a personal CI/CD pipeline (e.g., GitHub Actions) against a test app
- [ ] Triaging ZAP's automated alert output — separating true positives from noise, and documenting the reasoning

---

## Best Practices

- **Get explicit authorization before any active scan.** Active scanning sends real attack payloads and can modify application state or trigger unintended side effects — treat it with the same authorization requirements as manual penetration testing.
- **Start passive, then go active.** Passive scanning is safe to run broadly since it only analyzes existing traffic; active scanning should be deliberate and scoped.
- **Don't trust automated findings blindly.** Automated scanners produce false positives — triage and manually verify findings before including them in any report.
- **Use ZAP to complement manual testing, not replace it.** Business logic flaws and complex authorization issues often require manual investigation that automated scanning won't catch.
- **Be cautious with active scans in CI/CD.** Automated pipelines should only run active scans against dedicated test/staging environments, never production.

---

## Most Valuable Lessons Learned *(in progress)*

This section will grow with real findings as labs above are completed. Early conceptual takeaway:

- **Free and full-featured aren't mutually exclusive.** ZAP being fully open-source made it clear that cost isn't a real barrier to learning web application security — the barrier is time spent actually running scans and reading the findings.

I'd rather keep this honest and incremental than pad it — real scan results and findings will replace this note as work is completed.

---

## Resources

- [OWASP ZAP Official Documentation](https://www.zaproxy.org/docs/)
- ["Zap in Ten" Video Tutorial Series](https://www.youtube.com/playlist?list=PLEBitBW-Hlsv8cEIUntAO8st2UGhmrjUB)
- [OWASP Juice Shop (practice target)](https://owasp.org/www-project-juice-shop/)
- [TryHackMe: OWASP ZAP Room](https://tryhackme.com/room/owaspzap)
