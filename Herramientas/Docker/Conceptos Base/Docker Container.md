### ¿Qué es un Docker Container?
Un **Docker Container** es una **instancia en ejecución** de una Docker Image.

Representa un proceso aislado que se ejecuta con su propio:
- sistema de archivos
- red
- entorno

---

### Características clave
- Son **efímeros** (pueden crearse y destruirse fácilmente)
- Se ejecutan como procesos del sistema host
- Comparten el kernel del sistema operativo
- Pueden iniciarse, detenerse y eliminarse

---

### Ciclo de vida de un contenedor
1. Se crea a partir de una imagen
2. Se inicia
3. Se ejecuta
4. Se detiene
5. Puede eliminarse

---

### Para qué sirve un Docker Container
- Ejecutar aplicaciones de forma aislada
- Probar software sin afectar al sistema
- Ejecutar múltiples servicios en paralelo
- Simular entornos reales de producción

---

### Relación con otros conceptos
- Se crea a partir de una **Docker Image**
- Puede usar **volúmenes** para persistir datos

---

### Relacionado
- [[Docker]]
- [[Docker Image]]
- [[Docker Volume]]
- [[Herramientas/Docker/Viejo/Docker Compose]]