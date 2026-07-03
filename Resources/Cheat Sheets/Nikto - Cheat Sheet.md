# Nikto Cheat Sheet
**Web Server Vulnerability Scanning — Quick Reference**

---

## Core Workflow

1. Confirm authorization
2. Run a basic scan against the target
3. Scope with `-Tuning` if a full scan isn't needed
4. Save output for review/reporting
5. Manually verify findings before treating them as real

---

## Basic Commands

| Command | Purpose |
|---|---|
| `nikto -h example.com` | Basic scan |
| `nikto -h example.com -p 80,443` | Specific ports |
| `nikto -h https://example.com -ssl` | Force SSL/TLS scan |
| `nikto -h example.com -o report.html -Format html` | Save as HTML report |
| `nikto -h example.com -useproxy http://127.0.0.1:8080` | Route traffic through Burp Suite |

---

## Tuning Options (`-Tuning`)

*Scope a scan to specific check categories — useful for reducing noise or focusing testing.*

| Code | Category |
|---|---|
| `1` | Interesting file / seen in logs |
| `2` | Misconfiguration / default file |
| `3` | Information disclosure |
| `4` | Injection (XSS/script/HTML) |
| `5` | Remote file retrieval (inside web root) |
| `6` | Denial of service |
| `7` | Remote file retrieval (server-wide) |
| `8` | Command execution |
| `9` | SQL injection |
| `0` | File upload |
| `a` | Authentication bypass |
| `b` | Software identification |
| `c` | Remote source inclusion |
| `x` | Reverse tuning (exclude instead of include) |

Example: `nikto -h example.com -Tuning 1,2,3` limits the scan to file/misconfig/info-disclosure checks only.

---

## Other Useful Flags

| Flag | Purpose |
|---|---|
| `-Cgidirs <dir>` | Specify CGI directories to check |
| `-evasion <1-9>` | IDS evasion techniques (encoding tricks) |
| `-Pause <seconds>` | Delay between requests (reduce load/detection) |
| `-nossl` | Force non-SSL scanning |
| `-vhost <hostname>` | Scan a specific virtual host |

---

## Pro Tips

- **`-Tuning` is the single most useful flag for a portfolio walkthrough** — it shows intentional scoping rather than "ran the default scan."
- Nikto's version/banner checks produce frequent false positives — always cross-check flagged software versions manually.
- Route through Burp (`-useproxy`) to see exactly what requests Nikto sends — great for understanding what "noisy" actually looks like on the wire.
- Nikto is not designed to be stealthy — if practicing evasion concepts, treat `-evasion` as educational, not a guarantee.
- Combine with `-Pause` on fragile or low-resource lab targets to avoid crashing the service mid-scan.
