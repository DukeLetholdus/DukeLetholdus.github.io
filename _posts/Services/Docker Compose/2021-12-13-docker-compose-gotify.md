---
title: Gotify Docker Compose code
date: 2021-12-13 20:16:00 +/-TTTT
categories: [Services, Docker Compose]
tags: [service, gotify, docker, compose, code]     # TAG names should always be lowercase
---

```yml
---
version: "3"

services:
  gotify:
    image: gotify/server
    container_name: gotify
    ports:
      - 8140:80
    volumes:
      - "/home/leeuwera/docker/gotify/data:/app/data"
    restart: unless-stopped
```