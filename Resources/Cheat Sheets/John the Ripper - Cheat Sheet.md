# John the Ripper Cheat Sheet
**Password Cracking — Quick Reference**

---

## Core Workflow

1. Obtain hash(es) (authorized source only)
2. Identify or let John auto-detect the hash format
3. Choose attack mode (wordlist, rules, incremental)
4. Run and monitor; save session for long jobs
5. `--show` to view recovered plaintext passwords

---

## Basic Commands

| Command | Purpose |
|---|---|
| `john hashes.txt` | Crack using default wordlist + rules |
| `john --wordlist=rockyou.txt hashes.txt` | Dictionary attack with specific wordlist |
| `john --show hashes.txt` | Display already-cracked passwords |
| `john --status` | Check progress of a running/paused session |
| `john --restore` | Resume the most recent session |

---

## Hash Format Handling

| Command | Purpose |
|---|---|
| `john --list=formats` | List all supported hash formats |
| `john --format=NT hashes.txt` | Force NTLM format |
| `john --format=sha512crypt hashes.txt` | Force SHA-512 crypt format |
| `unshadow /etc/passwd /etc/shadow > combined.txt` | Merge Linux password files for cracking |

**Common formats:** `raw-md5`, `raw-sha1`, `NT` (Windows NTLM), `sha256crypt`, `sha512crypt`, `bcrypt`, `descrypt`

---

## Attack Modes

| Mode | Flag | Behavior |
|---|---|---|
| Wordlist | `--wordlist=<file>` | Tries each word in the list |
| Wordlist + Rules | `--wordlist=<file> --rules` | Applies mangling rules to each word (leetspeak, appended digits, casing) |
| Incremental (brute force) | `--incremental` | Tries all character combinations — slow, exhaustive |
| Single crack | `--single` | Uses account/GECOS info as candidate passwords (fast first pass) |

---

## Useful Flags

| Flag | Purpose |
|---|---|
| `--rules=<name>` | Use a specific named rule set instead of default |
| `--fork=<n>` | Run in parallel across n processes |
| `--session=<name>` | Name a session for later `--restore` |
| `--pot=<file>` | Specify a custom pot file (cracked password store) |

---

## Pro Tips

- **Identify the hash format before assuming John's auto-detection is right** — ambiguous hash lengths/prefixes can be misidentified.
- `--single` mode is fast and often cracks weak passwords tied to usernames before a full wordlist run is even needed.
- Long incremental jobs should always use `--session` — hardware issues or reboots shouldn't cost you progress.
- Rule-based mangling (`--rules`) frequently outperforms a bigger wordlist — understand *why* a rule works, not just that it does.
- `rockyou.txt` remains effective specifically because it's real breached password data — a good teaching point on password reuse.
