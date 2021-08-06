---
layout: post
tags: ["LAMP", "CentOS"]
title: "How to install LAMP on CentOS-7 Minimal with VirtualBox bridged adapter"
date: 2021-07-19T07:28:27+08:00
math: false
draft: false
---

**Prerequisites**
- VirtualBox-VM + CentOS-7 Minimal.
- Access to a user account with sudo or root privileges
- A terminal window or command line
- The yum and RPM package managers, included by default

**Make sure everything is up to date**
- sudo yum update
- sudo yum install httpd

**Start Apache and configure it**
- sudo systemctl start httpd.service
- sudo systemctl enable httpd.service

**Install MariaDB and configure it**
- sudo yum install mariadb-server mariadb
- sudo systemctl start mariadb
- sudo mysql_secure_installation (Y to everything + your preferred password)
- sudo systemctl enable mariadb.service

**Install PHP (I installed 7 due to needing to install WordPress)**
- Add EPEL and REMI Repository
- sudo yum -y install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
- sudo yum -y install https://rpms.remirepo.net/enterprise/remi-release-7.rpm
- sudo yum-config-manager --enable remi-php71
- sudo yum install php php-common php-opcache php-mcrypt php-cli php-gd php-curl php-mysql
- php -v (to check the version)
- sudo systemctl restart httpd.service

**Test PHP**
- Install nano with: sudo yum install nano
- sudo nano /var/www/html/info.php (or path used)
<?php phpinfo(); ?>
- http://localhost/info.php (or IP/info.php)

**Open routing with Firewall**
- sudo firewall-cmd --permanent --zone=public --add-service=http
- sudo firewall-cmd --permanent --zone=public --add-service=https
- sudo firewall-cmd --reload

You should be set!
