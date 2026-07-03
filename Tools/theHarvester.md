# theHarvester — OSINT Reconnaissance

**Category:** Open-Source Intelligence (OSINT) & Reconnaissance
**Difficulty:** Beginner
**License:** Open Source (GPL)

---

## Description

theHarvester is a reconnaissance tool that gathers publicly available information about a target organization — email addresses, subdomains, hostnames, employee names, and IP ranges — by querying public sources like search engines, certificate transparency logs, and DNS records. It's typically the first tool run in a penetration test, because it builds a picture of the target's external footprint before any active scanning begins.

Security professionals use theHarvester daily for:

- Building an initial attack surface map during the reconnaissance phase of a pentest
- Identifying employee email address patterns for phishing-simulation or social-engineering assessments
- Discovering forgotten or unofficial subdomains that may be under-secured
- Demonstrating to clients how much information about their organization is already public

---

## Key Features

- Aggregates data from many public sources in a single run (Google, Bing, crt.sh, Shodan, DNS, and more)
- Email address harvesting tied to a target domain
- Subdomain enumeration via certificate transparency logs and search engines
- Employee/name gathering from public sources (e.g., LinkedIn, when accessible)
- Optional Shodan integration for exposed host/service data
- DNS brute-forcing for additional subdomain discovery

---

## Common Commands

### Basic Domain Recon

```bash
# Search a single source
theHarvester -d example.com -b google

# Search all supported sources
theHarvester -d example.com -b all
```

### Limiting and Targeting Results

```bash
# Limit the number of results returned
theHarvester -d example.com -l 500 -b bing

# Search certificate transparency logs specifically for subdomains
theHarvester -d example.com -b crtsh
```

### Using Shodan Integration

```bash
# Requires a configured Shodan API key
theHarvester -d example.com -b shodan
```

### Saving Output

```bash
# Save results to a file for reporting
theHarvester -d example.com -b all -f results.html
```

---

## Hands-On Learning Path

OSINT proficiency comes from practicing on domains you own or that are explicitly designated for training — not from running recon against organizations without authorization, even though the data is public. Below is the progression most cybersecurity students use to build reps.

**Guided / legal practice targets**
- [ ] TryHackMe OSINT-focused rooms (e.g., "OSINT," "Wreath" reconnaissance phase)
- [ ] Running theHarvester against a personal domain or a domain you control, to see your own public footprint
- [ ] Comparing results across sources (Google vs. Bing vs. crt.sh) for the same domain, to understand why source diversity matters

**Concept-building exercises**
- [ ] Manually verifying a handful of theHarvester's harvested emails/subdomains against the live source, to build a habit of confirming automated output
- [ ] Mapping harvested subdomains to their live hosts using Nmap, connecting recon output to the next phase of a pentest
- [ ] Setting up a Shodan API key and comparing Shodan-sourced results to search-engine-sourced results for the same target

**Applied / integration practice**
- [ ] Documenting a full recon phase write-up: sources queried, findings, and how each finding would inform the next stage of an assessment
- [ ] Practicing the ethical boundary explicitly: identifying what theHarvester *could* return about a real organization vs. what would actually be appropriate to include in an authorized report

---

## Best Practices

- **Passive doesn't mean unrestricted.** Even though theHarvester queries public sources rather than touching the target directly, OSINT should still be scoped and authorized as part of a formal engagement.
- **Verify before you trust.** Public data can be stale, incorrect, or intentionally misleading — confirm significant findings (e.g., an email pattern or subdomain) before relying on them.
- **Use multiple sources.** Different search engines, DNS records, and certificate logs surface different information — relying on a single source will produce an incomplete picture.
- **Be mindful of personal data.** Employee names and emails are often the goal, but that data should only be used for the legitimate purpose of the assessment (e.g., phishing simulation design), never retained or used beyond scope.
- **Treat OSINT output as a starting point, not a conclusion.** Recon findings should feed into further, more targeted investigation — not be reported as final findings on their own.

---

## Most Valuable Lessons Learned *(in progress)*

This section will grow with real findings as labs above are completed. Early conceptual takeaway:

- **The attack surface is bigger than the org chart.** Seeing how much information is discoverable through public sources alone — before a single active scan — reframed how I think about an organization's real exposure versus its assumed exposure.

I'd rather keep this honest and incremental than pad it — real recon write-ups will replace this note as work is completed.

---

## Resources

- [theHarvester GitHub Repository](https://github.com/laramies/theHarvester)
- [OSINT Framework](https://osintframework.com/) — a broader map of OSINT tools and techniques
- [TryHackMe: OSINT Rooms](https://tryhackme.com/room/osint)
