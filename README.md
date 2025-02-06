# 🚀 Nextcloud Setup Guide

Introducing details of installing, configuring and managing Nextcloud on a private server or VPS.

### 🛠 Neccessary components
- **Operating System**: Ubuntu 20.04/22.04, Debian, CentOS...
- **Web Server**: Apache
- **Database**: MySQL/MariaDB
- **PHP**: PHP 8.x and neccessary module
- **SSL Certificate**: Let's Encrypt
- **Firewall**: Open neccessary ports (80, 443)
## 📌 Mục lục
- [Giới thiệu](#giới-thiệu)
- [Cài đặt Nextcloud](docs/setup.md)
- [Cấu hình Web Server](#cau-hinh-web-server)
  - [Apache](docs/apache.md)
  - [Nginx](docs/nginx.md)
- [Cấu hình SSL với Let's Encrypt](docs/ssl.md)
- [Backup và Restore dữ liệu](docs/backup.md)

## 📖 Introduction

Nextcloud is an open source platform that allows you to deploy a service to store and share personal data on a private server, similar to Google Drive or Dropbox but with complete control over the data. It is designed to secure information and meet the cloud storage needs of individuals, organizations, or businesses.

## 📥 Install Nextcloud
### Update and install neccessary packages
- Step 1: System update
    ```sh
    sudo apt update && sudo apt upgrade -y
    ```
- Step 2: Install Apache and neccessaries packages
  ```sh
  sudo apt install apache2 unzip curl -y
  sudo systemctl enable apache2
  sudo systemctl start apache2
  ```
- Step 3: Install Mariadb
  ```sh
  sudo apt install mariadb-server mariadb-client -y
  sudo systemctl enable mariadb
  sudo systemctl start mariadb
  ```
- Step 4: Config database
  #### Create database
  ```sh
  sudo mysql -u root -p
  ```
  ```sh
  ALTER USER 'root'@'localhost' IDENTIFIED BY 'root123@';
  FLUSH PRIVILEGES;
  EXIT;
  ```
  ```sh
  CREATE DATABASE nextcloud;
  CREATE USER 'nextcloud'@'localhost' IDENTIFIED BY 'nextcloud';
  GRANT ALL PRIVILEGES ON nextcloud.* TO 'nextcloud'@'localhost';
  FLUSH PRIVILEGES;
  EXIT;
  ```
- Step 4: Install PHP and extentions
  ```sh
  sudo apt install php libapache2-mod-php php-mysql php-gd php-xml php-mbstring php-curl php-zip php-intl php-bcmath php-imagick php-gmp php-apcu -y
  ```
- Step 5: Install Nextcloud
  ```sh
  cd /var/www/html
  sudo wget https://download.nextcloud.com/server/releases/latest-26.zip
  sudo unzip latest-26.zip
  sudo chown -R www-data:www-data nextcloud
  sudo chmod -R 755 nextcloud
  ```
## 🌐 Cấu hình Web Server
  #### Configure Apache
  ```sh
  sudo nano /etc/apache2/sites-available/nextcloud.conf
  ```
  #### File content
  ```sh
    <VirtualHost *:80>
      DocumentRoot /var/www/html/nextcloud
      ServerName yourdomain.com
  
      <Directory /var/www/nextcloud/>
          Require all granted
          AllowOverride All
          Options FollowSymLinks MultiViews
      </Directory>
  
      ErrorLog ${APACHE_LOG_DIR}/nextcloud_error.log
      CustomLog ${APACHE_LOG_DIR}/nextcloud_access.log combined
    </VirtualHost>
  ```
  #### Active configuration
  ```sh
  sudo a2ensite nextcloud.conf
  sudo a2enmod rewrite headers env dir mime
  sudo systemctl restart apache2
  ```
  #### Access Web and fill some neccessary information 
  - Open a browser and go to: `http://yourdomain.com` or `http://server-ip`
  - Set up an admin account, enter the newly configured database information.

## 🔒 Cấu hình SSL với Let's Encrypt
  ```sh
  sudo apt install certbot python3-certbot-apache
  ```  
  ```sh
  sudo nano /etc/apache2/sites-available/your_domain.conf
  ```
  ```sh
  ...
  ServerName your_domain
  ServerAlias www.your_domain
  ...
  ```
  ```sh
  sudo apache2ctl configtest
  ```
  ```sh
  sudo systemctl reload apache2
  ```
  ```sh
  sudo ufw allow 'Apache Full'
  ```
  ```sh
  sudo ufw delete allow 'Apache'
  ```
  ```sh
  sudo certbot --apache
  ```
  ```sh
  sudo ufw delete allow 'Apache'
  ```
