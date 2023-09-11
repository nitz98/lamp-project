

# WordPress Deployment Guide

This guide will help you set up a WordPress website on a Linux server with a LEMP stack (Linux, Nginx, MySQL, PHP), secure it with Let's Encrypt SSL/TLS certificates, optimize performance, and implement continuous integration/continuous deployment (CI/CD) using GitHub Actions.

## Step 1: Install LEMP Stack

1. Install Nginx, MySQL, and PHP:

   ```bash
   sudo apt install nginx mysql-server php-fpm php-mysql
   ```

2. Secure MySQL by running:

   ```bash
   sudo mysql_secure_installation
   ```

3. Create a Database: Create a MySQL database and user for WordPress. Note down the credentials.

4. Install Let's Encrypt: Install Certbot to manage SSL/TLS certificates:

   ```bash
   sudo apt install certbot python3-certbot-nginx
   ```

## Step 2: WordPress Setup

1. Download and Configure WordPress:

   - Download WordPress to your server:

     ```bash
     cd /var/www/html
     sudo wget https://wordpress.org/latest.tar.gz
     sudo tar -xzvf latest.tar.gz
     ```

   - Configure WordPress by creating a wp-config.php file using the sample configuration:

     ```bash
     sudo mv wordpress/wp-config-sample.php wordpress/wp-config.php
     ```

   - Edit wp-config.php and provide your database credentials.

2. Set Permissions:

   ```bash
   sudo chown -R www-data:www-data /var/www/html/wordpress
   sudo find /var/www/html/wordpress/ -type d -exec chmod 755 {} \;
   sudo find /var/www/html/wordpress/ -type f -exec chmod 644 {} \;
   ```

## Step 3: Nginx Configuration

1. Create an Nginx server block configuration file for your domain:

   ```bash
   sudo nano /etc/nginx/sites-available/yourdomain.com
   ```

   Example configuration:

   (Insert the Nginx configuration here)

2. Create a symbolic link to enable the configuration:

   ```bash
   sudo ln -s /etc/nginx/sites-available/yourdomain.com /etc/nginx/sites-enabled/
   ```

3. Test the Nginx configuration and restart Nginx:

   ```bash
   sudo nginx -t
   sudo systemctl restart nginx
   ```

## Step 4: Let's Encrypt SSL/TLS Certificate

1. Obtain and configure the SSL/TLS certificate:

   ```bash
   sudo certbot --nginx -d yourdomain.com -d www.yourdomain.com
   ```

2. Certbot will ask if you want to redirect HTTP traffic to HTTPS; choose your preference.

## Step 5: Performance Optimization

1. Enable Nginx Gzip Compression:

   Edit the Nginx configuration file:

   ```bash
   sudo nano /etc/nginx/nginx.conf
   ```

   Add the following lines inside the `http` block:

   (Insert the Nginx Gzip configuration here)

   Save and exit the file, then restart Nginx.


## Step 6: GitHub Actions for CI/CD

1. **GitHub Repository**:

   Create a new GitHub repository for your WordPress project.

2. **GitHub Actions Workflow**:

   Create a `.github/workflows/deploy.yml` file in your repository for your GitHub Actions workflow. Here's a sample configuration:

   ```yaml
   (Insert your GitHub Actions workflow YAML configuration here)
   ```


3. **Secrets**:

   In your GitHub repository settings, add  secrets: `KEY` (your SSH private key)  `USER` (ssh username)  `HOST` (ip or domain name of server) `PORT` (ssh port)  .

Now, every time you push to the main branch or raise pull request, GitHub Actions will deploy your WordPress site to your server.

This automated deployment process ensures your WordPress website is set up securely, with SSL/TLS, Nginx optimizations, and CI/CD in place.
```

