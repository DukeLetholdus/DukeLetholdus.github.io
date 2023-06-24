---
title: Dashy Docker Compose code
date: 2023-06-24 08:00:00 +/-TTTT
categories: [Services, Dashy]
tags: [service, dashy, docker, compose, code]     # TAG names should always be lowercase
---

```yml
---
version: "3.8"

services:
 dashy:
  image: lissy93/dashy
  container_name: Dashy
  volumes:
   - /home/leeuwera/docker/dashy/data:/app/public
  ports:
   - 8130:80
  environment:
   - NODE_ENV=production
   - UID=1000
   - GID=1000
  restart: always
```