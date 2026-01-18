---
name: multi-stage
description: Docker multi-stage builds for optimized images
---

# Multi-Stage Builds

## Concepto

Permite construir la aplicación en un contenedor y copiar solo los artefactos necesarios a un contenedor más pequeño y seguro.

## Ejemplo con Node.js

```dockerfile
# Stage 1: Build
FROM node:20-alpine AS builder

WORKDIR /app

COPY package*.json ./
RUN npm ci

COPY . .
RUN npm run build

# Stage 2: Production
FROM node:20-alpine

WORKDIR /app

# Instalar solo producción
COPY package*.json ./
RUN npm ci --only=production && npm cache clean --force

# Copiar build del stage anterior
COPY --from=builder /app/dist ./dist

EXPOSE 3000

CMD ["node", "dist/index.js"]
```

## Ejemplo con Go

```dockerfile
# Stage 1: Build
FROM golang:1.21-alpine AS builder

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main .

# Stage 2: Production
FROM alpine:latest

RUN apk --no-cache add ca-certificates

WORKDIR /root/

COPY --from=builder /app/main .

EXPOSE 8080

CMD ["./main"]
```

## Builder Pattern con BuildKit

```dockerfile
# syntax=docker/dockerfile:1.4
FROM alpine AS builder
RUN echo "build" > /artifact

FROM scratch
COPY --from=builder /artifact /
```
