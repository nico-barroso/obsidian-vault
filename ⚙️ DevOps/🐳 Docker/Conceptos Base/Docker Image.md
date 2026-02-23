### ¿Qué es una Docker Image?
Una **Docker Image** es una **plantilla inmutable** que contiene todo lo necesario para ejecutar una aplicación:
- código
- dependencias
- configuración
- sistema base

Las imágenes **no se ejecutan directamente**; sirven como base para crear contenedores.

---

### Características clave
- Son **inmutables** (no cambian una vez creadas)
- Se construyen por **capas**
- Se identifican por nombre y tag (`node:18`, `mysql:8.0`)
- Pueden almacenarse en registros (Docker Hub, privados, etc.)

---

### Para qué sirve una Docker Image
- Definir un entorno reproducible
- Garantizar consistencia entre entornos
- Compartir aplicaciones fácilmente
- Servir como base para múltiples contenedores

---

### Relación con otros conceptos
- Un **contenedor** es una instancia en ejecución de una imagen
- Las imágenes se crean normalmente a partir de un **Dockerfile**

---

### Relacionado
- [[Docker]]
- [[Docker Container]]
- [[Herramientas/Docker/Viejo/Dockerfile]]