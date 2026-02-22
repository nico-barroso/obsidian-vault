
|**Concepto clave**|**Nota útil**|
|---|---|
|**Persistencia**|Los datos se montan en el host para evitar su pérdida al borrar el contenedor.|

### Tipos de Volúmenes

1. **Anónimo:** Solo se indica la ruta interna. No se pueden referenciar fácilmente.
    
2. **De Anfitrión (Host):** Mapeo directo a una carpeta local.
    
3. **Nombrado:** Definidos en la sección `volumes` del compose; pueden ser referenciados por múltiples contenedores.
    

### Ejemplo en Compose

YAML

```
services:
  monguito:
    image: mongo
    volumes:
      - mongo-data:/data/db

volumes:
  mongo-data: # Definición del volumen nombrado
```

#docker #sistemas #devops #backend #dam #despliegue