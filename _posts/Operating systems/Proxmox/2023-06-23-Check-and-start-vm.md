---
title: Start VM if down
date: 2023-06-24 10:00:00 +/-TTTT
categories: [Operating Systems, Proxmox]
tags: [linux, proxmox, hypervisor, vm, crontab]     # TAG names should always be lowercase
---

# Check status of VM and start if necessary

## 1. Automate the startup of the VM

Make a bash script file
```bash
nano /home/restartwindows.sh
```

Put the following lines in the bash script file (where 100 is the VMID):
```bash
#!/bin/bash
qm status 100 | grep -q 'stopped' && qm start 100
```

Open crontab:
```bash
sudo nano /etc/crontab
```

Add the following line to the crontab file
```bash
* *     * * *   root    sh /home/restartwindows.sh
```