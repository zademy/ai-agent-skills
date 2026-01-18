---
name: networks
description: Docker networking concepts and configuration
---

# Docker Networks

## Tipos de Redes

```bash
# Bridge (por defecto)
docker network create --driver bridge mi-red-bridge

# Host
docker run --network host mi-imagen

# None
docker run --network none mi-imagen

# Overlay (swarm)
docker network create --driver overlay mi-red-overlay
```

## Gestion de Redes

```bash
docker network ls
docker network inspect mi-red-bridge
docker network connect mi-red-bridge mi-contenedor
docker network disconnect mi-red-bridge mi-contenedor
docker network rm mi-red-bridge
```

## Bridge en Compose

```yaml
version: '3.8'

services:
  app:
    build: .
    networks:
      - mi-red-bridge

  db:
    image: postgres:15
    networks:
      - mi-red-bridge

networks:
  mi-red-bridge:
    driver: bridge
    ipam:
      config:
        - subnet: 172.28.0.0/16
```
