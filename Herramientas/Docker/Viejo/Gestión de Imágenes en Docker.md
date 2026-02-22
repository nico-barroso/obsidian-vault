
|**Concepto clave**|**Nota útil**|
|---|---|
|**Docker Image**|Plantilla de solo lectura necesaria para crear contenedores.|

### Comandos de gestión de imágenes

- **Listar imágenes:** `docker images` muestra las imágenes disponibles localmente.
    
- **Descargar imágenes:** * `docker pull <imagen>`: Descarga la versión por defecto (`latest`).
    
    - `docker pull <imagen>:<tag>`: Ejemplo: `docker pull node:18`.
        
- **Eliminar imágenes:** `docker image rm <imagen>:<tag>` o `docker rmi <id_imagen>`.



---ATOMIZACIÓN:

## Configuración de Entornos Múltiples (Dev/Prod)

|**Concepto clave**|**Nota útil**|
|---|---|
|**Multi-stage/Env**|Uso de archivos específicos para desarrollo o producción.|

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

---

### Notas sugeridas para enlazar

- [[Virtualización vs Contenedores]]
    
- [[Comandos Linux Básicos]]
    
- [[Persistencia de Datos en DB]]
    


#docker #sistemas #devops #backend #dam #despliegue
