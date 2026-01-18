---
name: volumes
description: Docker volumes and data persistence
---

# Docker Volumes

## Tipos de Volúmenes

```bash
# Named volumes (recomendado)
docker volume create mi-volumen
docker run -v mi-volumen:/ruta/en/contenedor mi-imagen

# Bind mounts (para archivos/carpetas del host)
docker run -v /ruta/local:/ruta/en/contenedor mi-imagen

# Tmpfs mounts (datos en memoria)
docker run --tmpfs /ruta/en/contenedor mi-imagen
```

## Gestion de Volúmenes

```bash
# Listar volúmenes
docker volume ls

# Inspeccionar volumen
docker volume inspect mi-volumen

# Eliminar volumen (debe estar desconectado)
docker volume rm mi-volumen

# Eliminar volúmenes no utilizados
docker volume prune
```

## Volúmenes en Docker Compose

```yaml
version: '3.8'

services:
  app:
    build: .
    volumes:
      - mi-volumen:/app/data
      - ./config:/app/config:ro  # Solo lectura

  db:
    image: postgres:15
    volumes:
      - postgres_data:/var/lib/postgresql/data

  redis:
    image: redis:7
    volumes:
      - redis_data:/data

volumes:
  mi-volumen:
    driver: local
  postgres_data:
  redis_data:
```

## Copiar Datos

```bash
# Copiar desde contenedor a local
docker cp contenedor:/ruta/origen ./ruta/local

# Copiar desde local a contenedor
docker cp ./ruta/local contenedor:/ruta/destino
```
