# Common Commands

## Basic Domain Recon

```bash
# Search a single source
theHarvester -d example.com -b yahoo

# Search all supported sources
theHarvester -d example.com -b all
```
<img width="884" height="520" alt="Screenshot 2026-07-11 143150" src="https://github.com/user-attachments/assets/8de65c4f-696d-4501-8a2a-aedbd6d5cd39" />

<img width="884" height="542" alt="Screenshot 2026-07-11 143520" src="https://github.com/user-attachments/assets/a8fb97f8-5095-4e44-93a0-e412f9029a53" />

## Limiting and Targeting Results

```bash
# Limit the number of results returned
theHarvester -d example.com -l 500 -b yahoo

# Search certificate transparency logs specifically for subdomains
theHarvester -d example.com -b crtsh
```

<img width="881" height="562" alt="Screenshot 2026-07-11 145554" src="https://github.com/user-attachments/assets/9e8d7aa6-9556-4ac4-9632-ca60845635f7" />

<img width="885" height="560" alt="Screenshot 2026-07-11 143834" src="https://github.com/user-attachments/assets/df44a963-1244-44e4-9c80-d5a4b14a8323" />

## Using Shodan Integration

```bash
# Requires a configured Shodan API key
theHarvester -d example.com -b shodan
```

## Saving Output

```bash
# Save results to a file for reporting
theHarvester -d example.com -b all -f results.html
```

---
