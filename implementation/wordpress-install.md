# WordPress Installation on AWS EC2

## Prerequisites
- LAMP stack installed (see lamp-setup.md)
- Elastic IP assigned
- Domain DNS A record pointing to Elastic IP

## Step 1 — Create MySQL Database
```bash
sudo mysql -u root -p
```
```sql
CREATE DATABASE wordpress;
CREATE USER 'wpuser'@'localhost' IDENTIFIED BY '[strong-password]';
GRANT ALL PRIVILEGES ON wordpress.* TO 'wpuser'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

## Step 2 — Download WordPress
```bash
cd /var/www/html
sudo wget https://wordpress.org/latest.tar.gz
sudo tar -xzf latest.tar.gz
sudo mv wordpress/* .
sudo rm -rf wordpress latest.tar.gz
```

## Step 3 — Configure wp-config.php
```bash
sudo cp wp-config-sample.php wp-config.php
sudo nano wp-config.php
```
Update database settings and add hardening constants (see config/wp-config-hardening.md).

## Step 4 — Set Permissions
```bash
sudo chown -R apache:apache /var/www/html
sudo chmod -R 755 /var/www/html
sudo chmod 640 /var/www/html/wp-config.php
```

## Step 5 — Restart Services
```bash
sudo systemctl restart httpd
sudo systemctl restart php-fpm
```

## User Roles Created
| Role | Access |
|---|---|
| Administrator | Full wp-admin access |
| Author | Post creation only |
| Subscriber | Read only |

## Reference
- https://docs.aws.amazon.com/linux/al2023/ug/hosting-wordpress-aml-2023.html
