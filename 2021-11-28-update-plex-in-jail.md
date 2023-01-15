---
title: Update plex plugin in freeBSD jail
date: 2021-11-28 11:10:00 +/-TTTT
categories: [Operating Systems, FreeBSD]
tags: [freebsd, plex]     # TAG names should always be lowercase
---

## 1. Manual update

Navigate into the plex jail shell ande execute the following commands:
```bash
fetch -o PMS_Updater.sh https://raw.githubusercontent.com/mstinaff/PMS_Updater/master/PMS_Updater.sh
chmod 755 PMS_Updater.sh
./PMS_Updater.sh -vv -a
```

## 2. Automate the update
If not, make nano the default editor
```bash
setenv VISUAL /usr/local/bin/nano
```

create the bash script to be executed by cron and paste the commands in that file
```bash
nano /usr/scripts/updateplex.sh
```
```bash
#!/bin/sh
fetch -o PMS_Updater.sh https://raw.githubusercontent.com/mstinaff/PMS_Updater/master/PMS_Updater.sh
chmod 755 PMS_Updater.sh
./PMS_Updater.sh -vv -a
```

Now open the crontab folder and add the line to execute the script by root every sunday at 01:00
```bash
nano /etc/crontab
```
```bash
0 1 7 * * root /bin/sh /usr/scripts/updateplex.sh
```