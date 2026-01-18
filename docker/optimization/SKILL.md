---
name: optimization
description: Docker image optimization and best practices
---

# Docker Image Optimization

## Reducir Tamaño de Imagen

```dockerfile
# Usar imagen base ligera
FROM node:20-alpine  # vs node:20

# Instalar solo lo necesario
RUN apt-get update && apt-get install -y --no-install-recommends \
    ca-certificates \
    && rm -rf /var/lib/apt/lists/*

# Limpiar caches
RUN npm ci --only=production && npm cache clean --force

# Ordenar layers (lo que cambia menos primero)
FROM python:3.11-slim
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
```

## .dockerignore

```
# .dockerignore
node_modules
npm-debug.log
.git
.gitignore
.env
.env.*
Dockerfile
docker-compose*.yml
README.md
coverage
.nyc_output
*.log
```

## Mejores Prácticas

```dockerfile
# No ejecutar como root
RUN groupadd -r appgroup && useradd -r -g appgroup appuser
USER appuser

# Usar HEALTHCHECK
HEALTHCHECK --interval=30s --timeout=3s \
    CMD wget --quiet --tries=1 --spider http://localhost:3000/health || exit 1

# Labels para metadata
LABEL maintainer="dev@empresa.com" \
      version="1.0.0" \
      description="Mi aplicación"
```

## Análisis de Imagen

```bash
# Ver tamaño de capas
docker history mi-imagen:latest

# Inspeccionar imagen
docker inspect mi-imagen:latest

# Scan de vulnerabilidades
docker scan mi-imagen:latest
```
