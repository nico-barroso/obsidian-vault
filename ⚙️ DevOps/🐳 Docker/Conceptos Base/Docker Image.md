---
tags: [docker, imagenes]
category: DevOps
related: [[Docker Container]], [[Dockerfile]]
---

# Docker Image

Plantilla inmutable que contiene todo para ejecutar una aplicación:
- Código
- Dependencias
- Configuración
- Sistema base

## Características
- **Inmutables**: No cambian una vez creadas
- **Capas**: Se construyen por capas (layers)
- **Tags**: `node:18`, `mysql:8.0`
- **Registro**: Docker Hub o privados

## Relación
- Contenedor = instancia de una imagen
- Imagen = se crea desde Dockerfile

## Comandos
```bash
docker build .              # Construir
docker images              # Listar
docker pull nginx:latest   # Descargar
docker rmi <id>            # Eliminar
```

> Ver: [[Docker Container]], [[Dockerfile]]