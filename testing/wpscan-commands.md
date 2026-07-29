# WPScan Commands Used

## Plugin & Theme Enumeration (T-04, T-05)
```bash
wpscan --url https://[your-domain] --enumerate p,t,u
```

## With API Token (recommended for latest CVE data)
```bash
wpscan --url https://[your-domain] \
       --api-token [your-wpscan-api-token] \
       --enumerate p,t,u
```

## Options
| Flag | Purpose |
|---|---|
| --enumerate p | Enumerate installed plugins |
| --enumerate t | Enumerate active themes |
| --enumerate u | Enumerate usernames |

## Key Findings
| Item | Result |
|---|---|
| Plugin vulnerabilities | No critical CVEs in installed versions |
| WordPress version | Disclosure mitigated via headers |
| Username enumeration | No usernames exposed |

## References
- https://wpscan.com/
- https://wpscan.com/vulnerability-list
