# Security Approach — Defence-in-Depth

## Overview
Three-layer model: Network → Application → Observability

## Phase 1 — Network Security

| Port | Source | Purpose | Status |
|---|---|---|---|
| 80 HTTP | 0.0.0.0/0 | Public web | Open |
| 443 HTTPS | 0.0.0.0/0 | Secure web | Open |
| 22 SSH | /32 Admin IP | Admin only | Restricted |
| All others | Any | N/A | Blocked |

- Elastic IP: stable DNS across EC2 restarts
- OWASP Cloud Top 10 C6 mitigated
- Session Manager design-only (iam:CreateRole = paid AWS feature)

security-approach.mddocs/
| Plugin | Purpose | Standard |
|---|---|---|
| Two Factor Auth | TOTP Google Authenticator | NIST 800-63B |
| Limit Login Attempts | IP lockout 3 fails/20min | CWE-307 |
| Solid Security Basic | XML-RPC off, file detection | CIS |
| Sucuri Security | File integrity, audit log | WP Hardening |
| UpdraftPlus | Scheduled backups | Backup practice |
| Wordfence | Endpoint WAF + scanner | OWASP Top 10 |

wp-config.php:
```php
define('WP_HOME', 'https://[your-domain]');
define('WP_SITEURL', 'https://[your-domain]');
define('DISALLOW_FILE_EDIT', true);
```

## Phase 3 — Monitoring

- High CPU: >70% for 5min → SNS email
- Low CPU: <5% for 15min → SNS email
- Status Check: failure → SNS email
- Datadog: design only (IAM paid feature blocked)
