---
title: Custom systemctl service
date: 2023-01-13 15:45:00 +/-TTTT
categories: [Operating Systems, Linux]
tags: [linux, systemctl]     # TAG names should always be lowercase
---
# Make and run a custom systemctl service
## 1. Create the service file
Move to the folder where service files are located and use the touch command to create the file
```bash
cd /etc/systemd/system
touch myservice.service
```

## 2. Fill the service file
First, open the service file you just created
```bash
sudo nano myservice.service
```

Paste the code required to run your service into the service file.
Example:
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
This service file is what systemd uses to know our application exists and what to do with it. You should change the Description, ExecStart, WorkingDirectory and NODE_PORT statements to match your application. Your application may need more statements, add as needed.

## 3. Start the new service
Now we need to tell linux the new service exists and start it using the following comamnds
```bash
# Reload the daemon so it knows about the new file
sudo systemctl daemon-reload
# Start the service
sudo systemctl start myservice.service
```

Optional, to start the service on system startup use the following command:
```bash
sudo systemctl enable myservice.service
```

To check if the service is running:
```bash
systemctl status myserver.service
```
A example of what the status command will output:
```bash
● 30enserver.service - 30en server
     Loaded: loaded (/etc/systemd/system/30enserver.service; enabled; vendor preset: enabled)
     Active: active (running) since Wed 2023-01-11 21:07:57 UTC; 1 day 17h ago
   Main PID: 1070227 (node)
      Tasks: 7 (limit: 4531)
     Memory: 19.6M
        CPU: 1.001s
     CGroup: /system.slice/30enserver.service
             └─1070227 /usr/bin/node /var/www/truenas/30en/index.js

Jan 11 21:07:57 diensten systemd[1]: Started 30en server.
```

## 4. List running services
To make sure the service is running you can run the following command to list all services
```bash
systemctl list-units --type=service
```

## Sources
https://blog.r0b.io/post/running-node-js-as-a-systemd-service/