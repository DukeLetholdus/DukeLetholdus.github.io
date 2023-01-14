---
title: Uptime Kuma Docker Compose code
date: 2021-12-13 20:19:00 +/-TTTT
categories: [Services, Docker Compose]
tags: [service, uptime kuma, docker, compose, code]     # TAG names should always be lowercase
---

```yml
version: "3"

services:
  pihole:
    container_name: pihole
    image: pihole/pihole:latest
    ports:
      - "53:53/tcp"
      - "53:53/udp"
      - "67:67/udp"
      - "3003:80/tcp"
    environment:
      TZ: 'Europe/Amsterdam'
      WEBPASSWORD: 'rererorujuro'

    volumes:
      - '/home/growlithe/docker-volumes/pihole/data/etc-pihole/:/etc/pihole/'
      - '/home/growlithe/docker-volumes/pihole/data/etc-dnsmasq.d/:/etc/dnsmasq.d/'
    cap_add:
      - NET_ADMIN
    restart: unless-stopped
```