---
name: basics
description: Docker basics and best practices
---

# Docker Basics

## Dockerfile Básico

```dockerfile
FROM node:20-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .
RUN npm run build

EXPOSE 3000

CMD ["npm", "start"]
```

## Docker Compose

```yaml
version: '3.8'

services:
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=development
    volumes:
      - .:/app
      - /app/node_modules
    depends_on:
      - db

  db:
    image: postgres:15
    environment:
      POSTGRES_DB: mydb
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  postgres_data:
```

## Comandos Esenciales

```bash
# Construir imagen
docker build -t myapp:latest .

# Ejecutar contenedor
docker run -d -p 8080:3000 myapp:latest

# Ver contenedores en ejecución
docker ps

# Ver todos los contenedores
docker ps -a

# Detener contenedor
docker stop <container_id>

# Eliminar contenedor
docker rm <container_id>

# Ver logs
docker logs -f <container_id>

# Ejecutar comando en contenedor
docker exec -it <container_id> bash
```

## Multi-stage Build

```dockerfile
# Stage 1: Build
FROM node:20-alpine AS builder
WORKDIR /app
COPY . .
RUN npm run build

# Stage 2: Production
FROM node:20-alpine
WORKDIR /app
COPY --from=builder /app/dist ./dist
CMD ["node", "dist/index.js"]
```
