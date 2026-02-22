
|**Concepto clave**|**Nota útil**|
|---|---|
|**Port Mapping**|Vinculación de puertos entre el host y el contenedor.|
|**Networks**|Aislamiento y comunicación entre contenedores.|

### Publicación de puertos

Para acceder a un servicio (ej. MongoDB en `27017`) desde el ordenador anfitrión:

`docker create -p <puerto_host>:<puerto_contenedor> <imagen>`

Ejemplo: `docker create -p 27017:27017 mongo`.

### Comunicación entre contenedores

Los contenedores están aislados por defecto.

- **Listar redes:** `docker network ls`.
    
- Para que se comuniquen, deben agruparse en la misma red o usar herramientas de orquestación como [[Herramientas/Docker/Viejo/Docker Compose]].
    