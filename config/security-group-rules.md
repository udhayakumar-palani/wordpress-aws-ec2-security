# AWS Security Group Configuration

## Inbound Rules

| Type | Port | Source | Description |
|---|---|---|---|
| HTTP | 80 | 0.0.0.0/0 | Public web traffic |
| HTTPS | 443 | 0.0.0.0/0 | Secure web traffic |
| SSH | 22 | [admin-ip]/32 | Admin only |

## Verification
```bash
sudo nmap -sV -p 1-65535 [your-domain]
# Expected: 80/443 open, 22 filtered externally
```

## Key Decisions
- SSH /32 restriction: eliminates CVSS 9.8 Critical attack vector
- Elastic IP: stable DNS, no recycled IPs
- All other ports blocked by default

## Session Manager Design (Production)
```
1. Create IAM role with AmazonSSMManagedInstanceCore
2. Attach to EC2 instance profile
3. Remove port 22 from Security Group entirely
4. Access: AWS Console → Systems Manager → Session Manager
```
