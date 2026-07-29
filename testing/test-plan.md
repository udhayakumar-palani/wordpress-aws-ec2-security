# Security Testing — Structured Test Plan

## Summary: 14 Tests | 12 PASS | 1 PARTIAL | 0 FAIL

| ID | Test | Tool | Expected | Actual | Status |
|---|---|---|---|---|---|
| T-01 | Full port scan | Nmap | Only 80/443 open | Confirmed | PASS |
| T-02 | SSH non-admin IP | Terminal | TCP timeout | Timeout confirmed | PASS |
| T-03 | SSH admin IP | Terminal | Login success | Login succeeded | PASS |
| T-04 | Plugin CVE check | WPScan | No critical CVEs | None found | PASS |
| T-05 | Version enumeration | WPScan | Version hidden | Mitigated | PASS |
| T-06 | Brute-force login | Browser | Lockout after 3 | Locked at 3 | PASS |
| T-07 | MFA bypass | Browser | TOTP enforced | Bypass failed | PASS |
| T-08 | HTTP to HTTPS | Browser | 301 redirect | Confirmed | PASS |
| T-09 | File editor removed | Browser | Menus absent | Absent | PASS |
| T-10 | CloudWatch CPU alarm | AWS Console | Email < 5min | Received | PASS |
| T-11 | Status check alarm | AWS Console | OK state | Confirmed | PASS |
| T-12 | Non-admin login | Browser | No wp-admin | Redirected | PASS |
| T-13 | ZAP active scan | OWASP ZAP | 0 High alerts | 0 High, 3 Medium | PASS |
| T-14 | ZAP headers | OWASP ZAP | Headers present | CSP missing | PARTIAL |

## ZAP Medium Findings (T-13/T-14)

| Alert | CVSS | Remediation |
|---|---|---|
| X-Frame-Options missing | 4.3 | Add X-Frame-Options SAMEORIGIN in Apache |
| Apache version disclosure | 5.3 | Set ServerTokens Prod in httpd.conf |
| SameSite cookie missing | 4.3 | Add SameSite=Strict via wp-config.php |

## Evidence
- T-01, T-02, T-03: Appendix H (Nmap output)
- T-04, T-05: Appendix H (WPScan results)
- T-06: Appendix F (brute-force lockout screenshot)
- T-07: Appendix G (MFA prompt screenshot)
- T-10, T-11: Appendix J (CloudWatch alarms)
- T-13, T-14: Appendix I (ZAP alerts)
