---
tags:
  - cloud
  - arquitectura
  - despliegue
---

| Modelo      | Propiedad             | Acceso                   |
| :---------- | :-------------------- | :----------------------- |
| **Pública** | Proveedor (AWS/Azure) | Internet (Cualquiera).   |
| **Privada** | Organización          | Red Privada (Exclusivo). |
| **Híbrida** | Mixto                 | Conexión entre ambas.    |

## Clasificación
Se definen según quién posee la infraestructura y quién puede acceder a ella.

### 1. Nube Pública
* **Descripción:** Los recursos pertenecen a un proveedor externo (ej. AWS) y se entregan a través de Internet.
* **Hardware:** Compartido entre múltiples clientes.
* **Ventaja:** Coste inicial cero y escalabilidad casi infinita.

### 2. Nube Privada
* **Descripción:** Infraestructura dedicada exclusivamente a una sola organización.
* **Ubicación:** Puede estar *On-premise* (en tu edificio) o alojada por un tercero, pero el hardware no se comparte con otros clientes.
* **Ventaja:** Mayor control y aislamiento (ideal para datos muy sensibles).

### 3. Nube Híbrida
* **Descripción:** Combina nubes públicas y privadas permitiendo que los datos y aplicaciones se muevan entre ellas.
* **Caso de uso:** Mantener datos confidenciales en la privada y usar la pública para absorber picos de tráfico ("Cloud Bursting").