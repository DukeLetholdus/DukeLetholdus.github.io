---
title: Enter jail in FreeBSD
date: 2023-06-24 10:00:00 +/-TTTT
categories: [Operating Systems, FreeBSD]
tags: [freebsd, jail]     # TAG names should always be lowercase
---

## 1. Find Jail ID

The jail ID can be found with the command:
```bash
jls
```

## 2. Enter FreeBSD Jail

When the jail ID has been discovered you can enter the jail with the following command:
```bash
jexec ${jailID} /bin/tcsh
```
Where ${jailID} is the jail ID
