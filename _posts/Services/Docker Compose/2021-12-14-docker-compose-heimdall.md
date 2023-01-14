---
title: Heimdall Docker Compose code
date: 2021-12-14 10:46:00 +/-TTTT
categories: [Services, Docker Compose]
tags: [service, heimdall, docker, compose, code]     # TAG names should always be lowercase
---

```yml
---
version: "3"
services:
 heimdall:
  image: linuxserver/heimdall
  container_name: heimdall
  volumes:
   - /home/growlithe/docker-volumes/heimdall/data:/config
  environment:
   - PUID=1000
   - PGID=1000
   - TZ=Europe/Amsterdam
  ports:
   - "4100:80"
   - "4101:443"
  restart: unless-stopped
```