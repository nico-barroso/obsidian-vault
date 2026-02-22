---
tags:
  - aws
  - s3
  - almacenamiento
  - objetos
  - big-data
---


| Concepto Clave | Nota Útil |
| :--- | :--- |
| **Definición** | Servicio de almacenamiento de **objetos** altamente escalable. |
| **Estructura** | Plano (Flat). Se guardan objetos dentro de **Buckets**. |
| **Capacidad** | Prácticamente ilimitada. (Objeto individual máx: **5 TB**). |
| **Acceso** | Vía HTTP/HTTPS (API o URL), no se "monta" como un disco duro. |

## Definición y Conceptos Básicos
**Amazon S3** (Simple Storage Service) es almacenamiento para Internet. A diferencia de [[EBS (Elastic Block Store)]] (que son bloques/discos), S3 gestiona **Objetos**.
* **Bucket (Cubo):** Es el contenedor raíz.
    * *Regla Crítica:* El nombre debe ser **único a nivel global** (en todo el mundo, no solo en tu cuenta), ya que forma parte de la URL DNS.
* **Objeto:** Es el archivo en sí. Se compone de:
    * *Key (Clave):* El nombre del archivo.
    * *Value (Valor):* Los datos (bytes).
    * *Metadata:* Información sobre el archivo.
    * *Version ID:* Si el versionado está activo.



## Casos de Uso
* **Copias de seguridad (Backup):** Por su bajo coste y alta durabilidad.
* **Alojamiento de Medios:** Imágenes, vídeos y documentos para webs.
* **Alojamiento Web Estático:** Puedes alojar HTML/CSS/JS directamente sin servidor ([[EC2]]).
* **Data Lakes / Big Data:** Almacén central para datos estructurados y no estructurados.
* **Entrega de Software:** Distribución de binarios o parches.

## Clases de Almacenamiento ("Flavors")
S3 ofrece diferentes niveles de coste/rendimiento según la frecuencia de acceso:

1.  **S3 Standard:** Propósito general. Datos "calientes" de acceso frecuente.
2.  **S3 Intelligent-Tiering:** Mueve automáticamente los objetos entre capas según el uso (ahorro automático).
3.  **S3 Standard-IA (Infrequent Access):** Para datos que se usan poco, pero requieren acceso rápido cuando se piden. (Más barato almacenamiento, cobran por recuperación).
4.  **S3 One Zone-IA:** Igual que el anterior, pero guardado en **una sola AZ**. Menos redundante (-20% coste).
5.  **S3 Glacier:** Archivo profundo. Recuperación en minutos u horas.
6.  **S3 Glacier Deep Archive:** El más barato de todos. Para retención legal (años). Recuperación tarda ~12 horas.



## Precios (Facturación)
El modelo es "Pay-as-you-go". Te cobran por:
1.  **Almacenamiento:** GB/mes (precio depende de la clase elegida).
2.  **Transferencia de Datos (Saliente):** Lo que sale a Internet.
    * *Nota:* La transferencia entrante es **GRATIS**.
    * *Nota:* La transferencia hacia [[Amazon CloudFront]] o [[EC2]] (en la misma región) es **GRATIS**.
3.  **Solicitudes (Requests):** Número de peticiones (PUT, COPY, POST, LIST, GET).

## Diferencia Clave: S3 vs [[EBS]]

| Característica | Amazon S3 | Amazon EBS |
| :--- | :--- | :--- |
| **Tipo** | Almacenamiento de **Objetos**. | Almacenamiento de **Bloques**. |
| **Acceso** | Vía Web (HTTP/URL). Lento (latencia red). | Vía Sistema Operativo (Disco). Muy rápido. |
| **Escalado** | Ilimitado. | Limitado al tamaño del disco. |
| **Coste** | Mucho más barato. | Más caro (alto rendimiento). |
| **Uso Principal** | Fotos, Backups, Archivos Web. | S.O., Bases de Datos. |