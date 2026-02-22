---
tags:
  - aws
  - cloudfront
  - redes
  - cache
---

| Concepto Clave       | Nota Útil                                    |
| :------------------- | :------------------------------------------- |
| **Tipo de servicio** | CDN (Content Delivery Network) Global.       |
| **Características**  | Rápido, seguro, programable.                 |
| **Modelo**           | Autoservicio / Pago por uso (Pay-as-you-go). |
| **Relacionado**      | [[Content Delivery Network (CDN)]]           |

## Definición
**Amazon CloudFront** es el servicio de red de entrega de contenido ([[CDN]]) de AWS. Entrega datos, vídeos, aplicaciones y APIs a clientes de todo el mundo de forma segura, con baja latencia y altas velocidades de transferencia.

## Arquitectura de Caché en Capas
CloudFront no es plano, tiene una jerarquía para optimizar la retención de datos:

1.  **Ubicaciones de Borde (Edge Locations):**
    * Son los puntos más cercanos a los usuarios finales.
    * Almacenan el contenido **"popular"** (muy accedido) para entrega inmediata.
    * Hay cientos repartidas por todo el mundo.

2.  **Cachés de Borde Regionales (Regional Edge Caches):**
    * Se sitúan entre las Ubicaciones de Borde y el Servidor de Origen.
    * **Función:** Cuando un contenido deja de ser "muy popular", se elimina de la *Edge Location* para liberar espacio, pero se mantiene aquí.
    * **Ventaja:** Si un usuario vuelve a pedir ese contenido, se recupera desde la Regional Cache (más rápido y barato) en lugar de tener que ir hasta el servidor de origen (ej. [[Amazon S3]] o [[EC2]]).



## Características Principales
* **Seguridad:** Se integra con **AWS WAF** (Web Application Firewall) y **AWS Shield** (Protección DDoS) en el borde.
* **Orígenes Soportados:**
    * Servicios AWS: [[Amazon S3]], [[EC2]], [[Elastic Load Balancer]].
    * Servidores On-Premise (mediante IP pública).
* **Precios:**
    * Sin contratos ni pagos por adelantado.
    * Pagas por transferencia de datos saliente (Data Transfer Out) y solicitudes HTTP/HTTPS.