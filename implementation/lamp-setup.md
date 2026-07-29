# LAMP Stack Installation on Amazon Linux 2023

## Step 1 — Update System
```bash
sudo dnf update -y
```

## Step 2 — Install Apache
```bash
sudo dnf install -y httpd
sudo systemctl start httpd
sudo systemctl enable httpd
httpd -v  # Verify
```

## Step 3 — Install MariaDB
```bash
sudo dnf install -y mariadb105-server
sudo systemctl start mariadb
sudo systemctl enable mariadb
sudo mysql_secure_installation
mysql --version  # Verify
```

## Step 4 — Install PHP 8.x
```bash
sudo dnf install -y php php-mysqlnd php-fpm php-opcache php-xml php-gd php-mbstring
php --version  # Verify
```

## Step 5 — Set Permissions
```bash
sudo usermod -a -G apache ec2-user
sudo chown -R ec2-user:apache /var/www
sudo chmod 2775 /var/www
find /var/www -type d -exec sudo chmod 2775 {} \;
find /var/www -type f -exec sudo chmod 0664 {} \;
```

## Verify All Services
```bash
sudo systemctl status httpd
sudo systemctl status mariadb
cat /etc/os-release  # Confirm Amazon Linux 2023
```

## Reference
- https://docs.aws.amazon.com/linux/al2023/ug/ec2-lamp-amazon-linux-2023.html
