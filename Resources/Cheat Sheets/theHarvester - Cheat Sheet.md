# theHarvester Cheat Sheet
**OSINT Reconnaissance — Quick Reference**

---

## Core Workflow

1. Define target domain (owned or explicitly authorized)
2. Choose source(s) to query
3. Run and review harvested emails/subdomains/hosts
4. Manually verify significant findings before use
5. Feed confirmed subdomains into further recon (e.g., Nmap)

---

## Basic Commands

| Command | Purpose |
|---|---|
| `theHarvester -d example.com -b google` | Search a single source |
| `theHarvester -d example.com -b all` | Search all supported sources |
| `theHarvester -d example.com -l 500 -b bing` | Limit result count |
| `theHarvester -d example.com -b crtsh` | Subdomain enumeration via certificate transparency logs |
| `theHarvester -d example.com -b shodan` | Requires configured Shodan API key |
| `theHarvester -d example.com -b all -f results.html` | Save output to file |

---

## Common Source Flags (`-b`)

| Source | Data Type |
|---|---|
| `google` / `bing` / `duckduckgo` | Emails, hosts, general web presence |
| `crtsh` | Subdomains (certificate transparency) |
| `shodan` | Exposed hosts/services (requires API key) |
| `linkedin` | Employee names (availability varies) |
| `dnsdumpster` | DNS/subdomain data |
| `all` | Queries every configured source |

---

## Key Flags

| Flag | Purpose |
|---|---|
| `-d` | Target domain |
| `-b` | Source(s) to query |
| `-l` | Limit number of results |
| `-f` | Output file (HTML/XML) |
| `-n` | DNS resolution of discovered hosts |
| `-c` | DNS brute force for additional subdomains |

---

## Pro Tips

- **Run `-b all` last, not first** — start with 1-2 sources to understand output shape before drowning in combined results.
- Certificate transparency (`crtsh`) is one of the most reliable free subdomain sources — no API key required.
- Configure a Shodan API key early (`api-keys.yaml`) — it meaningfully expands exposed-service visibility.
- Cross-check harvested emails against a second source before treating a naming pattern (e.g., `first.last@domain.com`) as confirmed.
- Feed harvested subdomains directly into Nmap for the next reconnaissance phase — theHarvester tells you *what exists*, Nmap tells you *what's running on it*.
