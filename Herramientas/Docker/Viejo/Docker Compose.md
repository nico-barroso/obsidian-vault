
| **Concepto clave** | **Nota útil**                                            |
| ------------------ | -------------------------------------------------------- |
| **Orquestación**   | Definición y ejecución de aplicaciones multi-contenedor. |

### Configuración (docker-compose.yml)

Permite levantar servicios vinculados (links) y configurar entornos complejos.

YAML

```
version: "3.9"
services: 
  mi_app:
    build: . 
    ports: 
      - "3000:3000"
    links:
      - monguito
  monguito:
    image: mongo
    ports:
      - "27017:27017"
    environment:
      - MONGO_INITDB_ROOT_USERNAME=nico
```

- **Comando de despliegue:** `docker compose up` (ejecutar dentro de la carpeta del proyecto).
    



#docker #sistemas #devops #backend #dam #despliegue