---
title: Grafana Docker Compose code
date: 2021-12-13 20:17:00 +/-TTTT
categories: [Services, Docker Compose]
tags: [service, grafana, docker, compose, code]     # TAG names should always be lowercase
---

```yml
---
version: '3.7'

services:
 prometheus:
  image: prom/prometheus:v2.1.0
  volumes:
   - /home/leeuwera/docker/grafana/data/prometheus:/etc/prometheus
   - /home/leeuwera/docker/grafana/data/prometheus.yml:/etc/prometheus/prometheus.yml
  container_name: prometheus
  ports:
   - 9200:9090
  restart: unless-stopped

 grafana:
  image: grafana/grafana
  container_name: grafana
  user: "1000"
  depends_on:
   - prometheus
  ports:
   - 9201:3000
  volumes:
   - /home/growlithe/docker-volumes/grafana/data/grafana:/var/lib/grafana
  restart: unless-stopped
```