# WordPress on AWS EC2 — Security Hardening Project

> **Cloud Architecture and Security | NCI MSc Cyber Security | MSCCYB1_A**

A fully hardened WordPress deployment on AWS EC2, secured across three layers: **Network → Application → Observability**.

---

## System Architecture

```
Internet Users → Internet Gateway → Security Group → EC2 Instance → LAMP+WordPress → CloudWatch+SNS
                                    Port 80/443 open
                                    Port 22 /32 admin only
                                    All others blocked
```

See docs/architecture.xml for the full draw.io diagram.

---

## Security Controls

### Phase 1 — Network
- Security Group: HTTP/HTTPS public, SSH locked to /32 admin CIDR
- Elastic IP assigned for stable DNS
- SSH PEM key authentication

### Phase 2 — Application (6 Plugins)
- Two Factor Authentication — TOTP (NIST SP 800-63B)
- Limit Login Attempts Reloaded — IP lockout after 3 fails (CWE-307)
- Solid Security Basic — XML-RPC disabled, file change detection
- Sucuri Security — File integrity monitoring, audit log
- UpdraftPlus — Scheduled automated backups
- Wordfence Security — Endpoint WAF + malware scanner

wp-config.php hardening:
- WP_HOME / WP_SITEURL set to HTTPS
- DISALLOW_FILE_EDIT = true

### Phase 3 — Monitoring
- CloudWatch High CPU alarm: >70% for 5 min → SNS email
- CloudWatch Low CPU alarm: <5% for 15 min → SNS email
- CloudWatch Status Check alarm → SNS email

---

## Testing Results (14 Tests)

| ID | Test | Tool | Result |
|---|---|---|---|
| T-01 | Full port scan | Nmap | PASS — Only 80/443 open |
| T-02 | SSH from non-admin IP | Terminal | PASS — Timeout |
| T-03 | SSH from admin IP | Terminal | PASS — Login succeeded |
| T-04 | Plugin CVE check | WPScan | PASS — No critical CVEs |
| T-05 | Version enumeration | WPScan | PASS — Disclosure mitigated |
| T-06 | Brute-force login | Browser | PASS — Locked after 3 attempts |
| T-07 | MFA bypass attempt | Browser | PASS — TOTP enforced |
| T-08 | HTTP to HTTPS redirect | Browser | PASS — 301 + valid TLS |
| T-09 | File editor removed | Browser | PASS — Menu items absent |
| T-10 | CloudWatch CPU alarm | AWS Console | PASS — Email under 5 min |
| T-11 | Status check alarm | AWS Console | PASS — OK state confirmed |
| T-12 | Non-admin login | Browser | PASS — No wp-admin access |
| T-13 | ZAP active scan | OWASP ZAP | PASS — 0 High, 3 Medium |
| T-14 | ZAP headers check | OWASP ZAP | PARTIAL — Missing CSP noted |

---

## CVSS v3.1 Risk Ratings

| Finding | CVSS | Status |
|---|---|---|
| SSH open to 0.0.0.0/0 | 9.8 Critical | Mitigated |
| PHP file editor injection | 8.8 High | Mitigated |
| HTTP plaintext traffic | 7.4 High | Mitigated |
| No MFA on admin | 7.3 High | Mitigated |
| Unlimited login attempts | 7.5 High | Mitigated |
| WAF endpoint only | 4.5 Medium | Partial — Wordfence installed |
| X-Frame-Options missing | 4.3 Medium | Residual |
| Apache version disclosure | 5.3 Medium | Residual |
| Backup no EBS snapshot | 3.5 Low | Partial — UpdraftPlus installed |

---

## Repository Structure

- docs/ — architecture.xml, security approach, project plan
- config/ — security group rules, wp-config hardening, CloudWatch alarms
- testing/ — 14-test plan, Nmap commands, WPScan commands
- implementation/ — LAMP setup, WordPress install, plugin configuration
- screenshots/ — Evidence appendices A through M

---

## Team
- Udhaya Kumar Palani — Infrastructure Lead
- Aravind — Application Security and Live Demo
- Arun — Testing and Monitoring

NCI MSc Cyber Security — Cloud Architecture and Security CA — 2025
