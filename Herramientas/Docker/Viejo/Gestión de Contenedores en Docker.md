
|**Concepto clave**|**Nota útil**|
|---|---|
|**Lifecycle**|Proceso de creación, ejecución y visualización de contenedores.|

### Ciclo de vida básico

1. **Crear:** `docker create <imagen>`
    
    - Retorna un ID largo. Se puede usar el ID corto para comandos posteriores.
        
    - Opción con nombre: `docker create --name <nombre_personalizado> <imagen>`.
        
2. **Arrancar:** `docker start <id_o_nombre>`.
    
3. **Ejecutar (Crear + Arrancar):** `docker run <imagen>`.
    
    - `-d`: Modo _detached_ (ejecución en segundo plano).
        
    - `-e`: Definición de variables de entorno (ej. credenciales de DB).
        

### Visualización y Estado

- `docker ps`: Lista solo contenedores en ejecución.
    
- `docker ps -a`: Lista todos los contenedores (activos y detenidos).


#docker #sistemas #devops #backend #dam #despliegue