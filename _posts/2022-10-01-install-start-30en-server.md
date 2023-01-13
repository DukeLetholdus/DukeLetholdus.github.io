---
title: Start 30en Server
date: 2022-10-01 11:10:00 +/-TTTT
categories: [Websites, 30en]
tags: [linux, 30en, nohub, website]     # TAG names should always be lowercase
---

# Start the 30en Server

## 0. Dependancies

first install node.js:
```bash
sudo apt install nodejs
```

Install Node Package Manager to add packages:
```bash
sudo apt install npm
```
To check if node and npm installed correctly:
```bash
node -v
```
```bash
npm -v
```

## 1. Start 30en Server manually

To start 30en server in the background fill in the file path and use the following command:
```bash
nohup node /var/www/truenas/30en/index.js &
```
and
```bash
exit
```

## 2. Start 30en server on startup

Create a systemctl service file:
```bash
touch myservice.service
```
Go to "how to add systemctl service" article and fill the systemctl service with: 
```bash
[Unit]
Description=30en server

[Service]
#First path is where program is located. Second path is the file to execute
ExecStart=/usr/bin/node /var/www/truenas/30en/index.js
#Path where the file to execute is
WorkingDirectory=/var/www/truenas/30en
RestartSec=10
Restart=always
StandardOutput=syslog
StandardError=syslog
SyslogIdentifier=nodejs-my-server-example
Environment=PATH=/usr/bin:/usr/local/bin
# Customise port number port used by application
Environment=NODE_PORT=9090

[Install]
WantedBy=multi-user.target
```


## 3. Refresh 30en Server

Open the crontab:
```bash
crontab -e
```

On a new line paste the follwing code:
```bash
0 4 * * * systemctl restart 30en.service
```