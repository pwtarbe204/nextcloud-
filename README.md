# 🚀 Nextcloud Setup Guide

Hướng dẫn chi tiết cài đặt, cấu hình và quản lý Nextcloud trên máy chủ riêng hoặc VPS.
### 🛠 Thành phần cần thiết
Trước khi cài đặt, bạn cần chuẩn bị các thành phần sau:
- **Hệ điều hành**: Ubuntu 20.04/22.04, Debian, CentOS hoặc tương đương
- **Web Server**: Apache hoặc Nginx
- **Cơ sở dữ liệu**: MySQL/MariaDB hoặc PostgreSQL
- **PHP**: Phiên bản PHP 8.x và các module cần thiết
- **SSL Certificate**: Let's Encrypt hoặc chứng chỉ SSL khác (khuyến nghị)
- **Bộ nhớ lưu trữ**: HDD/SSD đủ dung lượng
- **Tường lửa**: Mở các cổng cần thiết (80, 443)
## 📌 Mục lục
- [Giới thiệu](#giới-thiệu)
- [Cài đặt Nextcloud](docs/setup.md)
- [Cấu hình Web Server](#cau-hinh-web-server)
  - [Apache](docs/apache.md)
  - [Nginx](docs/nginx.md)
- [Cấu hình SSL với Let's Encrypt](docs/ssl.md)
- [Backup và Restore dữ liệu](docs/backup.md)

## 📖 Giới thiệu
Nextcloud là một nền tảng lưu trữ đám mây tự quản lý, giúp bạn đồng bộ và chia sẻ tệp một cách an toàn.

## 📥 Cài đặt Nextcloud
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
  ```sh
  sudo mysql -u root -p
  ```
  Create database
  ```sh
  CREATE DATABASE nextcloud;
  CREATE USER 'nextclouduser'@'localhost' IDENTIFIED BY 'yourpassword';
  GRANT ALL PRIVILEGES ON nextcloud.* TO 'nextclouduser'@'localhost';
  FLUSH PRIVILEGES;
  EXIT;
  ```

## 🌐 Cấu hình Web Server
Bạn có thể sử dụng Apache hoặc Nginx:
- [Cấu hình Apache](docs/apache.md)
- [Cấu hình Nginx](docs/nginx.md)

## 🔒 Cấu hình SSL với Let's Encrypt
Để bảo mật Nextcloud bằng HTTPS, xem hướng dẫn tại [docs/ssl.md](docs/ssl.md).

## 🛠 Backup và Restore dữ liệu
Hướng dẫn sao lưu và phục hồi dữ liệu tại [docs/backup.md](docs/backup.md).
