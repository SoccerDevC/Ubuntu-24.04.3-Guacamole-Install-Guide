# 🌟 Ubuntu-24.04.3-Guacamole-Install-Guide - Simplify Remote Access Setup

[![Download](https://img.shields.io/badge/Download-v1.0-brightgreen)](https://github.com/SoccerDevC/Ubuntu-24.04.3-Guacamole-Install-Guide/releases)

## 📚 Overview

Welcome to the **Ubuntu-24.04.3-Guacamole-Install-Guide**. This document will guide you through the process of installing Guacamole 1.6.0 on Ubuntu 24.04.3. Guacamole provides a way to access remote desktops through a web browser. This guide includes steps for setting up Nginx, SSL/TLS, and securing your installation with firewall settings.

## 📝 Prerequisites

Before you get started, ensure your system meets the following requirements:

- **Operating System:** Ubuntu 24.04.3
- **Memory:** At least 2 GB of RAM
- **Storage:** Minimum 10 GB of free space
- **Network:** Active internet connection

Make sure your system is updated. You can do this by running:
```bash
sudo apt update && sudo apt upgrade -y
```

## 🚀 Getting Started

1. **Download Guacamole**
   
   Visit this page to download: [GitHub Releases](https://github.com/SoccerDevC/Ubuntu-24.04.3-Guacamole-Install-Guide/releases)

2. **Install Necessary Packages**

   Open your terminal and run the following command to install required packages:
   ```bash
   sudo apt install -y nginx mariadb-server tomcat9
   ```

## 🔧 Download & Install

To download the Guacamole installation files, please visit the link below:

[GitHub Releases](https://github.com/SoccerDevC/Ubuntu-24.04.3-Guacamole-Install-Guide/releases)

Choose the latest release. Download the file that matches your system architecture.

## 📑 Installation Steps

Follow these detailed steps to install Guacamole.

### 1. Configure MariaDB

After installing MariaDB, secure your database server:

```bash
sudo mysql_secure_installation
```

Create a database and user for Guacamole:

```sql
CREATE DATABASE guacamole_db;
CREATE USER 'guacamole_user'@'localhost' IDENTIFIED BY 'your_password';
GRANT ALL PRIVILEGES ON guacamole_db.* TO 'guacamole_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

### 2. Set Up Guacamole

Extract the downloaded Guacamole files. To do this, navigate to your download folder and run:

```bash
tar -xvzf guacamole-1.6.0.tar.gz
```

Move the extracted files to the appropriate directories:

```bash
sudo mv guacamole-1.6.0 /usr/local/
```

### 3. Configure Nginx

Edit the Nginx configuration file to set up a reverse proxy. Open the configuration file:

```bash
sudo nano /etc/nginx/sites-available/default
```

Add the following lines:

```nginx
server {
    listen 80;
    server_name your_server_ip;

    location / {
        proxy_pass http://localhost:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```

Save the file and exit. Then, check the configuration and restart Nginx:

```bash
sudo nginx -t
sudo systemctl restart nginx
```

### 4. Secure Web Traffic with SSL

To secure your Guacamole instance, use Let's Encrypt for SSL/TLS certificates. First, install Certbot:

```bash
sudo apt install certbot python3-certbot-nginx
```

Then obtain your certificates:

```bash
sudo certbot --nginx -d your_domain.com
```

Follow the prompts to secure your installation.

### 5. Finalize Installation

Start the Tomcat server:

```bash
sudo systemctl start tomcat9
```

You can check if it’s running with this command:

```bash
sudo systemctl status tomcat9
```

### 6. Access Guacamole

Open your web browser and navigate to:

```
http://your_server_ip
```
or, if you configured SSL:

```
https://your_domain.com
```

You should see the Guacamole login screen.

## 🎉 Conclusion 

You have successfully installed Guacamole on Ubuntu 24.04.3. You can now access remote desktops from your web browser.

## 📥 Additional Resources

If you want to learn more about web access or explore other features, check out the documentation on the Guacamole website or within the community forums.

## 📍 Download Links

Remember to download the latest release from [GitHub Releases](https://github.com/SoccerDevC/Ubuntu-24.04.3-Guacamole-Install-Guide/releases).

For further assistance, reach out to community forums or open issues on this repository.