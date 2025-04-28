# WordPress Website Setup Guide

This is a basic guide to set up your own WordPress site with a custom domain and server.

---

## 1. Domain

- [ ] Register a domain through a registrar (e.g., Namecheap, Google Domains, GoDaddy).
- [ ] Set up DNS settings:
  - [ ] Create an A record pointing to your server's public IP address. (1xx.1xx.1xxx)
- [ ] Install SSL certificate to enable HTTPS access:
  - [ ] Buy an SSL certificate (free) from the registrar.

---

## 2. Server

- [ ] Rent a cloud server in Amsterdam (AMS) for free (if possible):
  - Options: AWS EC2,  choose Ubantu or CentOS, a normal Linux System
- [ ] Secure your server:
  - [ ] Set up SSH key authentication.
  - [ ] Enable UFW firewall (open only ports 22, 80, 443).

---

## 3. Install Web Server Environment

Choose one environment:

- [ ] **LEMP stack** (Linux + Nginx + MySQL/MariaDB + PHP)
- **OR**
- [ ] **LAMP stack** (Linux + Apache + MySQL/MariaDB + PHP)

Install:
- [ ] Web server (Nginx or Apache)
- [ ] Database (MySQL or MariaDB)
- [ ] PHP and necessary PHP extensions

Check if the web server and PHP are working (test with a simple PHP page).

---

## 4. Install WordPress

- [ ] Download the latest WordPress package from [wordpress.org](https://wordpress.org/).
- [ ] Unzip and move WordPress files into the web server root directory (`/var/www/html` or your custom path).
- [ ] Set correct file permissions:
  - `sudo chown -R www-data:www-data /path/to/wordpress`
- [ ] Create a database and user for WordPress:
  - Use MySQL commands or a tool like phpMyAdmin.
- [ ] Configure `wp-config.php` with database info.
- [ ] Complete WordPress setup through the web installer (access via your domain).

---

## 5. Connect Your API (Optional)

If you need to insert your API into WordPress:

- [ ] Create a simple WordPress plugin **or**
- [ ] Edit the `functions.php` file of your theme.
- [ ] Use WordPress HTTP functions like:
  - `wp_remote_get()`
  - `wp_remote_post()`
- [ ] (Recommended) Cache API responses to avoid slowing down your site.

---

## 6. Final Check

- [ ] Test if your domain properly loads your WordPress site.
- [ ] Check if SSL (HTTPS) is working.
- [ ] Ensure your WordPress dashboard is accessible.
- [ ] Monitor your server resource usage occasionally (e.g., CPU, RAM).
# SSH Connection (Windows) and Basic Linux Operations

## 5. SSH Connection from Windows

- [ ] Install an SSH client:
  - or use Window Terminal
  - log in using connect <username>@ur domain(or ip address)
- [ ] Obtain server's public IP address.
- [ ] Open PuTTY and configure:
  - Host Name: `<your_server_ip>`
  - Port: `22`
  - Connection type: SSH
- [ ] Login with:
  - Username: `ubuntu` (or whatever the cloud provider specifies)
  - Private key file (if using key authentication)

---

## 6. Basic Linux Commands

- [ ] Update server packages:
  ```bash
  sudo apt update && sudo apt upgrade -y
  ```
- [ ] Install basic software packages:
  ```bash
  sudo apt install nginx mysql-server php-fpm php-mysql unzip
  ```
- [ ] Navigate between directories:
  ```bash
  cd /path/to/directory
  ls -al
  ```
- [ ] Create and edit files:
  ```bash
  nano filename.txt
  ```
- [ ] Restart services:
  ```bash
  sudo systemctl restart nginx
  sudo systemctl restart mysql
  ```
- Go to the previous directory
```bash
cd ../
```
- Restart 
```bash
reboot
```
---

# Upload Files from Your Computer to Your Server using FileZilla

## 7. Install and Connect FileZilla

- [ ] Download and install [FileZilla Client](https://filezilla-project.org/).
- [ ] Open FileZilla and set up a new site in Site Manager:
  - Host: `<your_server_ip>`
  - Port: `22`
  - Protocol: SFTP - SSH File Transfer Protocol
  - Logon Type: Normal (for password) or Key File (for SSH Key)
  - Username: `ur name`
  - Password or private key as needed.
- [ ] Connect to your server.

## 8. Upload Files

- [ ] Local computer files appear on the left.
- [ ] Server files appear on the right.
- [ ] Drag and drop files to upload into your server directories.

---
