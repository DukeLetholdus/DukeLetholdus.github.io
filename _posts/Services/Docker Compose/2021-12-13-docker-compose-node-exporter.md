---
title: Node Exporter Docker Compose code
date: 2021-12-13 20:18:00 +/-TTTT
categories: [Services, Docker Compose]
tags: [service, node exporter, docker, compose, code]     # TAG names should always be lowercase
---

```yml
---
version: '3.8'

services:
  node_exporter:
    image: quay.io/prometheus/node-exporter:latest
    container_name: node_exporter
    command:
      - '--path.rootfs=/host'
    pid: host
    restart: unless-stopped
    volumes:
      - '/:/host:ro,rslave'
    ports:
     - '9101:9100'
```