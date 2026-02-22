---
tags:
  - aws
  - cloud
  - redes
  - devops
  - sistemas
---

| Concepto Clave       | Nota Útil                                           |
| :------------------- | :-------------------------------------------------- |
| **Tipo de servicio** | DNS (Domain Name System) gestionado.                |
| **Características**  | Alta disponibilidad, escalabilidad, SLA del 100%.   |
| **Ámbito**           | [[Cloud Computing]] / [[Amazon Web Services (AWS)]] |

## Definición
Amazon Route 53 es un servicio web de Sistema de Nombres de Dominio ([[DNS (Domain Name System)]]) escalable y de alta disponibilidad en la nube. Está diseñado para ofrecer a desarrolladores y empresas una forma fiable y rentable de dirigir a los usuarios finales a las aplicaciones de Internet.

Funciona traduciendo nombres de dominio legibles (ej. `www.ejemplo.com`) en direcciones IP numéricas (ej. `192.0.2.1`) que los ordenadores utilizan para conectarse entre sí.



## Políticas de Enrutamiento (Routing Policies)
Route 53 utiliza diferentes políticas para determinar cómo responder a las consultas DNS:

* **Enrutamiento simple (Simple Routing):** Para un único recurso que cumple una función para un dominio.
* 
* **Enrutamiento ponderado (Weighted Round Robin):** Distribuye el tráfico entre múltiples recursos según proporciones (pesos) definidas.
* 
* **Enrutamiento de latencia (Latency Routing):** Dirige el tráfico a la región que proporciona la menor latencia al usuario.
* 
* **Enrutamiento de geolocalización (Geolocation Routing):** Enruta el tráfico basándose en la ubicación geográfica de los usuarios (país, continente, etc.).
* 
* **Enrutamiento de geoproximidad (Geoproximity Routing):** Enruta el tráfico basándose en la ubicación de los recursos y, opcionalmente, desplaza el tráfico de una ubicación a otra (requiere *Route 53 Traffic Flow*).
* 
* **Enrutamiento de conmutación por error (Failover Routing):** Se utiliza para configuraciones activo-pasivo (disaster recovery); dirige el tráfico a un recurso alternativo si el principal no está saludable.
* 
* **Enrutamiento de respuesta con varios valores (Multivalue Answer Routing):** Permite devolver varios registros (direcciones IP) aleatorios para una misma consulta, mejorando la disponibilidad (similar a un balanceo de carga simple).

## Relacionado
- [[DNS]] (Sistema de Nombres de Dominio)
- [[Alta Disponibilidad (HA)]]
- [[Balanceadores de Carga]]