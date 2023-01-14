---
title: Install and edit crontab in Linux
date: 2021-11-28 11:10:00 +/-TTTT
categories: [Operating Systems, Linux]
tags: [linux, crontab, schedule]     # TAG names should always be lowercase
---

# Install and edit crontab in Linux

## 1. Install Crontab

To install Crontab:
```bash
sudo apt install cron
```

Enable Crontab to start on boot:
```bash
sudo systemctl enable --now cron
```

To check if Crontab is running:
```bash
sudo systemctl status cron
```

## 2. Open Crontab

To open Crontab
```bash
crontab -e
```

To open Crontab with other editor use:
```bash
export VISUAL=EDITOR; crontab -e
```
List of common editors to use in command above:
* nano
* vim

## Edit Crontab
The format for Crontab is 5 input fields for time, separated by tab or space, and a command
<br/><br/>
![Crontab Format](/assets/img/cron/schedule-cron-fields.png)

| Field            | Format of valid values |
|------------------|------------------------|
| minute           | 0-59                   |
| Hour             | 0-23                   |
| Day of the Month | 1-31                   |
| Month            | 1-12                   |
| Dayt of the week | 1-7                    |

| Sample Schedule                | Cron job format |
|--------------------------------|-----------------|
| Every minute                   | * * * * *       |
| Every Saturday at 23:45        | 45 23 * * 6     |
| Every Monday at 09:00          | 0 9 * * 1       |
| Every Weekday at 22:00         | 0 22 * * 1-5    |
| Every 1st of December at 12:00 | 0 12 1 12 *     |