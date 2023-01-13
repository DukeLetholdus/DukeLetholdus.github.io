---
title: Create a LEMP stack on linux
date: 2022-10-01 18:21:00 +/-TTTT
categories: [Operating Systems, Linux]
tags: [linux, lemp, nginx, webserver]     # TAG names should always be lowercase
---
# Create a LEMP (Linux Nginx MySQL PHP) stack for hosting websites

## 0. Preparations
Firstly, make sure your system is up to date
```bash
sudo apt update
sudo apt upgrade
```

It is advisable to disable the ufw firewall. Only do this if the network is secured.
```bash
sudo ufw disable
```

## 1. Install Nginx
The Nginx package can be installed with the following command
```bash
sudo apt install nginx
```

you can now acces the default page on your browser. Find the ip of your server
```bash
ip addr show
```
And go the the ip adress in your browser. You should see the default Nginx page

## 2. Install MySQL

## 3. Install PHP
Now you can install PHP to process code and generate dynamic content for the web server
```bash
sudo apt install php8.1-fpm php-mysql -y
```

## 4. Configure Nginx to use PHP and host your website
To host multiple websites, a configuration file is created for each and included in /etc/nginx/nginx.conf. Configuration files created in /etc/nginx/sites-enabled are automatically included
</br></br>
To create and edit the configuration file:
```bash
sudo nano /etc/nginx/sites-available/your_domain.conf
```
Now you need to populate this file with the code required to host your website.</br> 
Example:
```bash
server {
    listen 80;
    server_name your_domain www.your_domain;
    root /var/www/your_domain;

    index index.html index.htm index.php;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
     }

    location ~ /\.ht {
        deny all;
    }

}
```
Here’s what each of these directives and location blocks do:

* listen — Defines what port Nginx will listen on. In this case, it will listen on port 80, the default port for HTTP.
* root — Defines the document root where the files served by this website are stored.
* index — Defines in which order Nginx will prioritize index files for this website. It is a common practice to list index.html files with higher precedence than index.php files to allow for quickly setting up a maintenance landing page in PHP applications. You can adjust these settings to better suit your application needs.
* server_name — Defines which domain names and/or IP addresses this server block should respond for. Point this directive to your server’s domain name or public IP address.
* location / — The first location block includes a try_files directive, which checks for the existence of files or directories matching a URL request. If Nginx cannot find the appropriate resource, it will return a 404 error.
* location ~ \.php$ — This location block handles the actual PHP processing by pointing Nginx to the fastcgi-php.conf configuration file and the php8.1-fpm.sock file, which declares what socket is associated with php8.1-fpm.
* location ~ /\.ht — The last location block deals with .htaccess files, which Nginx does not process. By adding the deny all directive, if any .htaccess files happen to find their way into the document root, they will not be served to visitors.

You will now have to test your configuration for syntax error by running the following command:
```bash
sudo nginx -t
```
If any errors are reported, go back to your configuration file to review its contents before continuing.

When you are ready, reload Nginx to apply the changes:
```bash
sudo systemctl reload nginx
```

Your website is now online

## 5. Make sure Nginx uses PHP
To check if Nginx uses the PHP processor, Create a file called index.php in the default website located in /var/www/html and open this file
```bash
sudo touch /var/www/html/index.php
sudo nano /var/www/html/index.php
```

Copy the following code into index.php
```html
<?php
phpinfo();
```
You will now see the PHP info when you go to the IP of your webserver followed by index.php
```html
http://20.0.2.30/index.php
```

## Sources
https://www.digitalocean.com/community/tutorials/how-to-install-linux-nginx-mysql-php-lemp-stack-on-ubuntu-22-04