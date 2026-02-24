---
tags: [docker, compose, orquestacion]
category: DevOps
related: [[Docker]]
---

# Docker Compose

Herramienta para definir y ejecutar aplicaciones multi-contenedor.

## Ejemplo docker-compose.yml

```yaml
version: '3.8'
services:
  web:
    image: nginx
    ports:
      - "80:80"
  db:
    image: postgres
    environment:
      POSTGRES_PASSWORD: secret
```

## Comandos

```bash
docker-compose up -d      # Arrancar
docker-compose down       # Parar
docker-compose logs -f   # Ver logs
```

> Ver: [[Docker]]
