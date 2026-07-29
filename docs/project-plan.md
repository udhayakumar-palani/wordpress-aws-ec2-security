# Project Plan

| # | Task | Phase | Depends On | Status |
|---|---|---|---|---|
| 1 | Launch EC2 instance | Network | — | Complete |
| 2 | Allocate Elastic IP | Network | 1 | Complete |
| 3 | Configure Security Group | Network | 1 | Complete |
| 4 | Install LAMP stack | Application | 1,3 | Complete |
| 5 | Deploy WordPress | Application | 4 | Complete |
| 6 | Point DNS to Elastic IP | Application | 2,5 | Complete |
| 7 | Configure HTTPS in wp-config | Application | 5,6 | Complete |
| 8 | DISALLOW_FILE_EDIT | Application | 7 | Complete |
| 9 | Two Factor Authentication | Application | 5 | Complete |
| 10 | Limit Login Attempts | Application | 5 | Complete |
| 11 | Solid Security Basic | Application | 5 | Complete |
| 12 | Sucuri Security | Application | 5 | Complete |
| 13 | UpdraftPlus backup | Application | 5 | Complete |
| 14 | Wordfence WAF | Application | 5 | Complete |
| 15 | User roles (Author, Subscriber) | Application | 5 | Complete |
| 16 | CloudWatch High CPU alarm + SNS | Monitoring | 1 | Complete |
| 17 | CloudWatch Low CPU alarm | Monitoring | 16 | Complete |
| 18 | CloudWatch Status Check alarm | Monitoring | 16 | Complete |
| 19 | Security testing (Nmap, WPScan, ZAP) | Testing | 3-18 | Complete |
| 20 | Datadog design | Monitoring | — | Design Only |
| 21 | Session Manager design | Network | — | Design Only |
