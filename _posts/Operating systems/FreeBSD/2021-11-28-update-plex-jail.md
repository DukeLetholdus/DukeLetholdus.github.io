---
title: Update Plex in FreeBSD jail
date: 2021-11-28 11:11:00 +/-TTTT
categories: [Operating Systems, FreeBSD]
tags: [freebsd, plex, cron]     # TAG names should always be lowercase
---

## 1. Manual update

Navigate into the plex jail shell ande execute the following commands:
```bash
fetch -o PMS_Updater.sh https://raw.githubusercontent.com/mstinaff/PMS_Updater/master/PMS_Updater.sh
chmod 755 PMS_Updater.sh
./PMS_Updater.sh -vv -a
```