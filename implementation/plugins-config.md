# WordPress Security Plugins — Configuration

## 1. Two Factor Authentication
Install: Plugins > Add New > Search "Two Factor"
Configure: Users > Profile > Two-Factor Options > Enable Authenticator App
- Scan QR code with Google Authenticator
- Verify: login triggers TOTP prompt after password

## 2. Limit Login Attempts Reloaded
Install: Plugins > Add New > Search "Limit Login Attempts Reloaded"
Configure: Settings > Limit Login Attempts
```
Allowed retries:  3
Lockout duration: 20 minutes
Repeat lockout:   24 hours after 4 lockouts
Email on lockout: Yes
```
Verify: Enter wrong password 3 times — lockout message appears.

## 3. Solid Security Basic
Install: Plugins > Add New > Search "Solid Security"
Key settings:
- Disable XML-RPC
- Hide WordPress version string
- File change detection alerts
- Security activity log

## 4. Sucuri Security
Install: Plugins > Add New > Search "Sucuri Security"
Features active:
- Audit Log Monitor
- File Integrity Monitor (WordPress core)
- Blacklist Monitor (SiteCheck)
- Security Hardening recommendations

## 5. UpdraftPlus
Install: Plugins > Add New > Search "UpdraftPlus"
Configure: Settings > UpdraftPlus Backups
```
Files:    Weekly backup
Database: Daily backup
Remote:   Email delivery
Include:  All files + MySQL database
```
Verify: Settings > UpdraftPlus > Existing Backups > completed entry visible.

## 6. Wordfence Security
Install: Plugins > Add New > Search "Wordfence Security"
Features:
- Web Application Firewall (WAF) active
- Malware Scanner — no threats found
- Real-time threat intelligence (community)
- IP and country blocking
- Login security (complements Limit Login Attempts)
