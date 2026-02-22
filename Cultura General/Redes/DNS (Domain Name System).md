---
tags:
  - redes
  - dns
  - aws-exam
  - infraestructura
  - devops
---

| Concepto Clave       | Nota Útil                                                                 |
| :------------------- | :------------------------------------------------------------------------ |
| **Definición**       | Sistema jerárquico que traduce nombres legibles a IPs numéricas.          |
| **Analogía**         | La guía telefónica de Internet.                                           |
| **Puerto/Protocolo** | Puerto **53**. UDP (búsquedas) / TCP (transferencias/respuestas grandes). |
| **Ámbito**           | [[Redes]] / [[Amazon Route 53]]                                           |

## 1. Fundamentos Técnicos
El DNS elimina la necesidad de memorizar direcciones IP (`142.250.184.4`) permitiendo el uso de nombres (`google.com`).
* **FQDN (Fully Qualified Domain Name):** Nombre absoluto que incluye la raíz. Termina técnicamente en punto (ej: `www.ejemplo.com.`).
* **Protocolo de Transporte:**
    * **UDP (Default):** Para consultas estándar (rápidas y ligeras).
    * **TCP:** Se usa si la respuesta excede el tamaño del paquete UDP o para **Transferencias de Zona** (replicación entre servidores DNS).

## 2. Jerarquía del DNS (El Árbol)
La resolución se lee de **derecha a izquierda**: `.` $\to$ `com` $\to$ `google` $\to$ `www`.



1.  **Zona Raíz (Root Zone `.`):** Punto de inicio. Gestionada por 13 servidores lógicos mundiales.
2.  **TLD (Top-Level Domain):** Extensiones de dominio.
    * *Genéricos (gTLD):* .com, .org, .net.
    * *Geográficos (ccTLD):* .es, .mx, .uk.
3.  **Dominio de Segundo Nivel:** Nombre de la organización (ej: `amazon`, `google`).
4.  **Subdominio:** Recurso específico (ej: `www`, `api`, `blog`).

## 3. Proceso de Resolución
Flujo cuando un cliente busca `www.tienda.com`:



1.  **Stub Resolver (Cliente):** Busca en caché local o archivo `hosts`. Si no está, consulta al Resolver.
2.  **Resolver Recursivo (ISP/Google 8.8.8.8):** Realiza la búsqueda jerárquica:
    * Pregunta al **Root**: "¿Quién gestiona `.com`?" $\to$ Respuesta: Servidores TLD (.com).
    * Pregunta al **TLD**: "¿Quién gestiona `tienda.com`?" $\to$ Respuesta: Servidores Autoritativos (ej. [[Amazon Route 53]]).
    * Pregunta al **Autoritativo**: "¿IP de `www`?" $\to$ Respuesta: `1.2.3.4`.
3.  **Respuesta Final:** El Resolver entrega la IP al cliente y la guarda en caché por el tiempo del [[#5. TTL (Time To Live)|TTL]].

## 4. Tipos de Registros DNS (Records)
Lista de registros esenciales para configuración y examen.

| Tipo | Nombre | Función | Ejemplo |
| :--- | :--- | :--- | :--- |
| **A** | Address | Nombre $\to$ **IPv4**. (Estándar). | `api.web.com` $\to$ `54.21.10.1` |
| **AAAA** | Quad A | Nombre $\to$ **IPv6**. | `api.web.com` $\to$ `2001:db8::1` |
| **CNAME** | Canonical Name | Nombre $\to$ **Otro Nombre**. <br>⚠️ **Prohibido en la raíz (Apex)**. | `m.web.com` $\to$ `mobile.web.com` |
| **MX** | Mail Exchange | Servidores de **correo**. Usa prioridad numérica. | `web.com` $\to$ `smtp.gmail.com` |
| **NS** | Name Server | Delega la autoridad de la zona (quién es tu DNS). | `web.com` $\to$ `ns-1.awsdns.com` |
| **TXT** | Text | Verificación de propiedad y seguridad email (SPF/DKIM). | "google-site-verification..." |
| **ALIAS** | **AWS Exclusive** | Extensión de Route 53. Como un CNAME pero **SÍ funciona en la raíz**. | `web.com` $\to$ `elb.amazonaws.com` |

### Diferencia Clave: CNAME vs ALIAS (Examen AWS)
* **CNAME:** Estándar DNS. No puede coexistir con otros registros en el mismo nombre. Por eso **no se puede usar en el dominio raíz** (`tienda.com`).
* **ALIAS:** Puntero interno de AWS. **Permitido en la raíz**. Gratuito. Apunta dinámicamente a recursos AWS ([[Elastic Load Balancer]], [[Amazon CloudFront]], [[Amazon S3]]).

## 5. TTL (Time To Live)
Duración del registro en la memoria caché de los resolvers.
* **TTL Alto (ej. 24h):** Menos tráfico al servidor DNS, propagación de cambios lenta.
* **TTL Bajo (ej. 60s):** Propagación rápida, mayor carga/coste en el servidor DNS.