
| **Concepto clave** | **Nota útil**                                                    |
| ------------------ | ---------------------------------------------------------------- |
| **Dockerfile**     | Archivo de configuración para construir imágenes personalizadas. |

### Estructura de un Dockerfile (Node.js)

Dockerfile

```
FROM node:18                  # Imagen base
RUN mkdir -p /home/app        # Ejecuta comandos en la construcción
COPY . /home/app              # Copia archivos del host al contenedor
WORKDIR /home/app             # Define el directorio de trabajo
EXPOSE 3000                   # Documenta el puerto de escucha
CMD ["node", "index.js"]      # Comando de ejecución principal
```



#docker #sistemas #devops #backend #dam #despliegue