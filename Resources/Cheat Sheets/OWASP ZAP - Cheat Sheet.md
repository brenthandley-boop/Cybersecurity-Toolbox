# OWASP ZAP Cheat Sheet
**Web Application Security Scanning — Quick Reference**

---

## Core Workflow

1. Configure browser proxy (default `127.0.0.1:8080`) or use ZAP's built-in browser launch
2. Spider the target to map its structure
3. Run a **passive scan** (automatic, non-intrusive)
4. Run an **active scan** only on authorized targets
5. Review and triage alerts by risk level
6. Export report

---

## Docker Quick-Start Commands

| Command | Purpose |
|---|---|
| `docker run -t owasp/zap2docker-stable zap-baseline.py -t https://example.com` | Passive baseline scan |
| `docker run -t owasp/zap2docker-stable zap-full-scan.py -t https://example.com -r report.html` | Full scan (passive + active) with report |
| `docker run -t owasp/zap2docker-stable zap-api-scan.py -t <openapi-url> -f openapi` | API-focused scan |

---

## zap-cli Quick Reference

| Command | Purpose |
|---|---|
| `zap-cli start` | Start the ZAP daemon |
| `zap-cli spider <url>` | Crawl target to map structure |
| `zap-cli active-scan <url>` | Run active scan (authorized targets only) |
| `zap-cli alerts` | List discovered alerts |
| `zap-cli report -o report.html -f html` | Generate HTML report |

---

## Alert Risk Levels

| Level | Meaning |
|---|---|
| **High** | Likely exploitable, needs immediate attention |
| **Medium** | Real concern, verify and prioritize |
| **Low** | Minor issue or hardening opportunity |
| **Informational** | No direct risk, useful context |
| **False Positive** | Manually confirmed as not applicable — mark to reduce noise |

---

## Scan Types

| Type | Behavior | Risk Level |
|---|---|---|
| **Passive Scan** | Analyzes traffic already sent — no payloads injected | Safe for any traffic ZAP observes |
| **Active Scan** | Sends attack payloads to test for vulnerabilities | Can modify app state — authorization required |
| **Spider** | Crawls links to map the application | Generally safe, but generates real traffic/requests |
| **AJAX Spider** | Crawls JavaScript-heavy apps via a real browser engine | Slower, more thorough on modern SPAs |

---

## Pro Tips

- **Passive scan runs automatically as you browse** — you get free findings just by using the proxy manually, no active scan needed.
- Use the **HUD** (Heads-Up Display) for manual testing — it overlays ZAP's findings directly in the browser window.
- Always run Spider before Active Scan — an active scan can only test what the spider (or manual browsing) has discovered.
- Automate baseline scans in CI/CD only against dedicated test/staging environments — never production.
- Compare ZAP's automated findings against manual Burp Suite testing of the same app — they don't always catch the same issues.
