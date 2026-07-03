# Burp Suite Cheat Sheet
**Web Application Security Testing — Quick Reference**

---

## Setup

| Step | Detail |
|---|---|
| Proxy listener | `127.0.0.1:8080` (default) |
| Browser config | Set HTTP/HTTPS proxy to Burp's listener, or use FoxyProxy extension |
| CA Certificate | `http://burpsuite` (while proxy active) → download & install to intercept HTTPS |
| Scope | **Target → Scope** — add target, then right-click traffic → "Add to scope" |
| Filter noise | **Proxy → HTTP history** → filter bar → "Show only in-scope items" |

---

## Core Workflow

1. Configure browser proxy (`127.0.0.1:8080`) and install CA cert for HTTPS
2. Define **Target Scope** before doing anything else
3. Toggle **Intercept** on, browse the target application
4. Send interesting requests to **Repeater** (`Ctrl+R`) for manual editing
5. Use **Intruder** for automated payload testing (brute force, fuzzing)
6. Use **Comparer** to diff two responses; **Decoder** to encode/decode values
7. Document findings as you go — screenshot request + response + what you changed

---

## Key Tools

| Tool | Shortcut | Best For |
|---|---|---|
| **Proxy** | — | Intercepting & modifying live traffic |
| **Repeater** | `Ctrl+R` | Manual, repeated payload testing on one request |
| **Intruder** | `Ctrl+I` | Brute force, fuzzing, parameter enumeration |
| **Comparer** | — | Diffing two responses (e.g., valid vs. invalid session) |
| **Decoder** | — | Encoding/decoding (Base64, URL, hex, hashing) |
| **Sequencer** | — | Analyzing session token randomness/entropy |
| **Extender** | — | Installing BApp Store extensions |
| **Logger** | — | Full traffic log, searchable, across all tools |

---

## Intruder Attack Types

| Type | Behavior | Use Case |
|---|---|---|
| **Sniper** | One payload set, one position at a time | Testing a single parameter |
| **Battering ram** | Same payload in all positions simultaneously | Same value needed in multiple fields |
| **Pitchfork** | Multiple payload sets, one position each, run in parallel | Paired username/password lists |
| **Cluster bomb** | Multiple payload sets, all combinations tested | Full brute-force of two+ independent fields |

---

## Repeater Keyboard Shortcuts

| Shortcut | Action |
|---|---|
| `Ctrl+Space` | Send request |
| `Ctrl+Shift+B` | Send request (background) |
| `Ctrl+Shift+F` | Beautify/format request body |
| `Ctrl+F` | Search within request/response |

---

## Common Use Cases

- Authorization / access control bypass testing (IDOR)
- SQL injection / XSS manual confirmation before automating with sqlmap
- Parameter tampering (price, quantity, role fields)
- Session token analysis and hijacking attempts (Sequencer)
- CSRF token validation testing

---

## Pro Tips

- **Always define Target Scope first** — prevents accidental out-of-scope traffic and keeps HTTP history readable.
- **Match and Replace** (Proxy → Options) automates repetitive header/value changes across all requests.
- **Community Edition rate-limits Intruder** — for large attacks, throttle expectations or use targeted, smaller payload sets.
- Use **"Send to Repeater" from Proxy history** rather than rebuilding requests manually.
- Right-click any request → **"Copy as curl command"** to move a request outside Burp for scripting.

---

## Community vs. Professional (know the difference)

| Feature | Community | Professional |
|---|---|---|
| Proxy / Repeater / Decoder / Comparer / Sequencer | ✅ | ✅ |
| Intruder speed | Throttled | Full speed |
| Automated Scanner | ❌ | ✅ |
| Automation Framework (CI/CD) | ❌ | ✅ |
