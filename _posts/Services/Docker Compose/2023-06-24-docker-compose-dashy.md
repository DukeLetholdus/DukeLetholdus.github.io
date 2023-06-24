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
    # Pass in your config file below, by specifying the path on your host machine
    volumes:
      - /home/leeuwera/docker/dashy/data/conf.yml:/app/public/conf.yml
    ports:
      - 8130:80
    environment:
      - NODE_ENV=production
      - UID=1000
      - GID=1000
    restart: always
    healthcheck:
      test: ['CMD', 'node', '/app/services/healthcheck']
      interval: 1m30s
      timeout: 10s
      retries: 3
      start_period: 40s
```