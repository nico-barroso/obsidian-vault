---
tags: [docker, contenedores]
category: DevOps
related: [[Docker Image]], [[Volumen]], [[Docker Compose]]
---

# Docker Container

Instancia en ejecución de una [[Docker Image]].

## Características
- **Ephemeros**: Se crean y destruyen fácilmente
- Comparten el kernel del SO host
- Aislamiento: sistema de archivos, red, entorno propios

## Ciclo de vida
1. Crear (desde imagen)
2. Iniciar
3. Ejecutar
4. Detener
5. Eliminar

## Comandos básicos
```bash
docker run nginx           # Crear y ejecutar
docker ps                  # Ver activos
docker stop <id>          # Detener
docker rm <id>            # Eliminar
```

> Ver: [[Docker Image]], [[Volumen]], [[Docker Compose]]