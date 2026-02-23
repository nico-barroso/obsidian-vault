
| **Concepto clave**  | **Nota útil**                                             |
| ------------------- | --------------------------------------------------------- |
| **Multi-stage/Env** | Uso de archivos específicos para desarrollo o producción. |

### Dockerfile.dev

Suele incluir herramientas de recarga en caliente como `nodemon`.

Dockerfile

```
FROM node:18
RUN npm i -g nodemon
WORKDIR /home/app
EXPOSE 3000
CMD ["nodemon", "index.js"]
```

### Ejecución con archivo específico

Para levantar un entorno de desarrollo con un archivo YAML personalizado:

`docker compose -f docker-compose-dev.yml up`

#docker #sistemas #devops #backend #dam #despliegue