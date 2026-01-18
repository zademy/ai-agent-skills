---
name: security
description: Docker security best practices
---

# Docker Security

## Buenas Prácticas

```dockerfile
# No usar usuario root
FROM node:20-alpine

RUN addgroup -g 1000 appgroup && \
    adduser -u 1000 -G appgroup -s /bin/sh -D appuser

USER appuser
```

## Escaneo de Vulnerabilidades

```bash
# Docker Scout
docker scout cves mi-imagen:latest

# Trivy
trivy image mi-imagen:latest
```

## Políticas de Seguridad

```yaml
# docker-compose.yml
services:
  app:
    build: .
    security_opt:
      - no-new-privileges:true
    read_only: true
    cap_drop:
      - ALL
    cap_add:
      - NET_BIND_SERVICE
```

## Secrets en Swarm

```yaml
version: '3.8'

services:
  app:
    image: mi-app:latest
    secrets:
      - db_password

secrets:
  db_password:
    file: ./secrets/db_password.txt
```
