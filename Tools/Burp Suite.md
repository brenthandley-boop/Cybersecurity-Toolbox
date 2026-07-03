# Burp Suite — Web Application Security Testing

**Category:** Web Application Security
**Difficulty:** Intermediate to Advanced
**License:** Free (Community Edition) / Paid (Professional)

---

## Description

Burp Suite is the industry-standard toolkit for testing the security of web applications. It works as an intercepting proxy, sitting between your browser and the target application so every request and response can be viewed, paused, and modified before it's sent or received.

Security professionals use Burp Suite daily for:

- Manual web application penetration testing
- Finding logic flaws and injection points automated scanners miss
- Testing authentication and session management
- Understanding what real exploitation attempts look like at the HTTP request level

---

## Key Features

- **Proxy** — intercepts and lets you inspect/modify HTTP(S) traffic in real time
- **Repeater** — resend a modified request repeatedly to test how the application responds
- **Intruder** — automate sending requests with varying payloads (e.g., for fuzzing or parameter testing)
- **Target/Scope** — defines what's in-bounds for testing to avoid touching out-of-scope systems
- **Decoder** — encode/decode data (Base64, URL encoding, hashing) found in requests
- **Extensions (BApp Store)** — add community-built tools for specialized testing

---

## Common Workflows

Burp Suite is GUI-driven rather than command-line, so instead of commands, here are the core workflows:

```
1. Configure browser to route traffic through Burp's proxy (default: 127.0.0.1:8080)
2. Install Burp's CA certificate to intercept HTTPS traffic
3. Turn on Intercept and browse the target application
4. Send an interesting request to Repeater (Ctrl+R)
5. Modify parameters/headers in Repeater and resend to observe application behavior
6. Use Target > Scope to restrict testing to authorized hosts only
```

---

## Best Practices

- **Never test outside written authorization.** Burp Suite is an active testing tool — using it against an application you don't have explicit permission to test can have serious legal consequences, regardless of intent.
- **Set your scope before you start.** Defining Target/Scope early prevents accidentally sending traffic to systems that aren't part of the engagement.
- **Understand a request before modifying it.** Reading and understanding the baseline request/response is more valuable early on than jumping straight to automated tools like Intruder.
- **Document as you go.** Screenshot and log interesting findings (request, response, and what you changed) immediately — it's easy to lose track of which modification produced which result.
- **Practice only on intentionally vulnerable applications** (e.g., OWASP Juice Shop, DVWA, PortSwigger's own labs) until you're working under a formal, authorized engagement.

---

## Hands-On Learning Path

Burp Suite proficiency is built through repetition against intentionally vulnerable, legal-to-attack targets. Below is the progression most cybersecurity students and self-taught practitioners use — the same one I'm working through. Checked items reflect labs actually completed; this list updates as real work is done.

**PortSwigger Web Security Academy** *(free, built by the makers of Burp — the most widely used starting point)*
- [ ] SQL injection — retrieving hidden data via a login bypass
- [ ] Cross-site scripting (XSS) — reflected, stored, and DOM-based labs
- [ ] Authentication — username enumeration and password brute-forcing with Intruder
- [ ] Access control vulnerabilities — IDOR and privilege escalation labs
- [ ] Cross-site request forgery (CSRF) — bypassing basic CSRF token validation
- [ ] Business logic vulnerabilities — exploiting flawed application assumptions

**OWASP Juice Shop** *(intentionally vulnerable app, gamified with a scoreboard)*
- [ ] Intercepting and modifying a request to manipulate a price or quantity
- [ ] Identifying and exploiting a broken access control challenge
- [ ] Using Repeater to test input validation on a form field

**DVWA (Damn Vulnerable Web Application)** *(classic, security-level-adjustable practice target)*
- [ ] Low-security SQL injection via Burp's Repeater
- [ ] Command injection testing at increasing security levels
- [ ] Comparing how the same attack behaves at "low" vs. "high" security settings — a good way to see what real mitigations look like in practice

---

## Most Valuable Lessons Learned *(in progress)*

This section will grow with real findings and screenshots as labs above are completed. Early takeaway so far:

- **Proxies make the invisible visible.** Seeing a normal login request broken down field-by-field made it clear how much of web security testing is really just careful, methodical observation — not a special hacking mindset, but a disciplined one.

I'd rather keep this honest and incremental than pad it — full walkthroughs with real findings will replace these notes as labs are actually completed.

---

## Resources

- [PortSwigger Web Security Academy](https://portswigger.net/web-security) — free, hands-on labs (where I'm building reps)
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [Burp Suite Official Documentation](https://portswigger.net/burp/documentation)
- [OWASP Juice Shop (practice target)](https://owasp.org/www-project-juice-shop/)
