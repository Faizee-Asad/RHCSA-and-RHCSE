# ✅ Project Configure the LAMP Stack on a VM 
# 🧰 Project Title: Deploying a PHP Blog on Amazon Linux EC2 with LAMP Stack

*👨‍💻 By: Asad Faizee*
*Cloud & Linux Administrator | AWS Enthusiast | DevOps Learner*

# 📌 Overview

This project demonstrates the complete setup and deployment of a PHP-based blog application using the LAMP stack (Linux, Apache, MySQL, PHP) on an Amazon EC2 instance running Amazon Linux 2023. It showcases my ability to configure cloud infrastructure, manage a Linux environment, install and configure software components, and troubleshoot real-time web server issues.

# 🧱 Tech Stack

| Component   | Technology        |
| ----------- | ----------------- |
| OS          | Amazon Linux 2023 |
| Web Server  | Apache (httpd)    |
| Programming | PHP               |
| Database    | MariaDB (MySQL)   |
| Hosting     | AWS EC2           |
| Git Project | Simple PHP Blog   |

# 📈 Goals

Launch an EC2 instance and install a LAMP stack
Deploy a PHP blog from a GitHub repository
Configure Apache and MySQL
Resolve common issues (e.g., HTTP 500, permission errors)
Test the application from a public browser

# 🔧 Step-by-Step Implementation

## 🟢 1. Launch EC2 (Amazon Linux 2023)

- Choose Amazon Linux 2023 AMI
- Instance type: t2.micro (free tier)
- Key pair: Create/download .pem file
- Security group: Allow ports 22 (SSH) and 80 (HTTP)

## 🟢 2. Connect via SSH

```
ssh -i "your-key.pem" ec2-user@<EC2-Public-IP>
```
## 🟢 3. Install LAMP Stack
```
sudo dnf update -y
sudo dnf install httpd php php-mysqlnd mariadb105-server git -y

sudo systemctl enable --now httpd
sudo systemctl enable --now mariadb
```


## 🟢 4. Configure Apache
```
sudo systemctl start httpd
sudo systemctl enable httpd
```

## Test it with:

```
echo "<?php phpinfo(); ?>" | sudo tee /var/www/html/index.php
```
Visit: http://<EC2-Public-IP>

## 🟢 5. Secure MySQL & Create DB
```
sudo systemctl enable --now mariadb
sudo mysql_secure_installation
```
Then:

```
sudo mysql -u root -p

CREATE DATABASE blog;
CREATE USER 'bloguser'@'localhost' IDENTIFIED BY 'StrongPass123!';
GRANT ALL PRIVILEGES ON blog.* TO 'bloguser'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

## 🟢 6. Clone and Configure PHP Blog

```
cd /var/www/html
sudo rm -rf *
sudo git clone https://github.com/Philipinho/Simple-PHP-Blog.git .
sudo chown -R apache:apache /var/www/html
```
Update connect.php or config.php:

```
$host = 'localhost';
$user = 'bloguser';
$pass = 'StrongPass123!';
$dbname = 'blog';
```
Import SQL file:

```
mysql -u bloguser -p blog < /var/www/html/database.sql
```

## 🟢 7. Fix Permissions & Restart

```
sudo chown -R apache:apache /var/www/html
sudo chmod -R 755 /var/www/html
sudo systemctl restart httpd
```