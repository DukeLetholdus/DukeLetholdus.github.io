---
title: Uptime Kuma Docker Compose code
date: 2022-10-02 16:20:00 +/-TTTT
categories: [Services, Docker Compose]
tags: [service, uptime kuma, docker, compose, code]     # TAG names should always be lowercase
---

```yml
---
version: "3.1"

services:
 uptime-kuma:
  image: louislam/uptime-kuma:1
  container_name: uptime-kuma
  volumes:
   - /home/leeuwera/docker/uptime/data:/app/data
  ports:
   - 3001:3001
  restart: unless-stopped
```