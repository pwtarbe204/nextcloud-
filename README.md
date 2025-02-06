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
- Update and install necessary packages
  ```sudo apt update && sudo apt upgrade -y```

## 🌐 Cấu hình Web Server
Bạn có thể sử dụng Apache hoặc Nginx:
- [Cấu hình Apache](docs/apache.md)
- [Cấu hình Nginx](docs/nginx.md)

## 🔒 Cấu hình SSL với Let's Encrypt
Để bảo mật Nextcloud bằng HTTPS, xem hướng dẫn tại [docs/ssl.md](docs/ssl.md).

## 🛠 Backup và Restore dữ liệu
Hướng dẫn sao lưu và phục hồi dữ liệu tại [docs/backup.md](docs/backup.md).
