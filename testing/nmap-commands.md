# Nmap Commands Used

## Full Port Scan (T-01, T-02)
```bash
# From external non-admin IP
sudo nmap -sV -p 1-65535 [your-domain]
```

Expected output:
```
PORT      STATE    SERVICE   VERSION
80/tcp    open     http      Apache httpd 2.4.x
443/tcp   open     https     Apache httpd 2.4.x
22/tcp    filtered ssh
All others: filtered/closed
```

## SSH Test from Admin IP (T-03)
```bash
# From authorised /32 admin IP
nmap -sV -p 22 [your-domain]
# Expected: 22/tcp open ssh OpenSSH 8.x
```

## Interpretation
- open: port accessible
- filtered: blocked by Security Group (working as intended)
- closed: reachable but no service

## CVSS Context
- SSH open to 0.0.0.0/0 (pre-hardening): CVSS 9.8 Critical
- SSH to /32 admin only (post-hardening): Residual risk Low
