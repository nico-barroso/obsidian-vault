
---
tags:
  - aws
  - cloud
  - moc
  - indice
  - infraestructura
---
# AWS - Amazon Web Services

| Concepto Clave | Nota Útil |
| :--- | :--- |
| **Definición** | Plataforma líder de servicios en la nube. |
| **Modelo** | Principalmente [[IaaS]], [[PaaS]] y Serverless. |
| **Estructura** | Global (Regiones y AZs). |
| **Relacionado** | [[Cloud - Modelos de Servicio y Responsabilidad]] |

## ¿Qué es AWS?
**Amazon Web Services (AWS)** es la plataforma en la nube más completa y adoptada del mundo. Ofrece más de 200 servicios integrales desde centros de datos a nivel global. Permite a las empresas acceder a infraestructura tecnológica bajo demanda (pago por uso) sin necesidad de inversión física inicial.

## 1. Infraestructura Global
La potencia de AWS reside en su distribución física, diseñada para la tolerancia a fallos.
* **[[AWS - Regiones y Avaialbilty Zones (AZ)]]**: Áreas geográficas independientes.
* **[[Availability Zone]] (AZ):** Centros de datos aislados dentro de cada región.

## 2. Servicios Principales (Por Categoría)

### 🖥️ Computación
El "cerebro" de la nube. Desde máquinas virtuales hasta código sin servidor.
* **[[EC2]]**: Servidores virtuales escalables. Se lanzan usando una **[[Amazon Machine Image (AMI)]]**.
* **[[Amazon Lambda]]**: Computación *serverless* (ejecuta código sin gestionar servidores).
* **Costes:** Para ahorrar en cómputo estable, se utilizan **[[Instancias reservadas]]**.

### 💾 Almacenamiento
Dónde guardamos los datos.
* **[[Amazon S3]]**: Almacenamiento de objetos (archivos, backups, web estática).
* **[[EBS (Elastic Block Store)]]**: Discos duros persistentes de bloque para conectar a EC2.

### 🌐 Redes y Entrega de Contenido
Cómo conectamos los servicios entre sí y con Internet.
* **[[Amazon VPC]]**: Tu red privada virtual aislada en la nube.
    * Para salir a internet: **[[Internet Gateway (IGW)]]**.
    * Para controlar el tráfico: **[[AWS - Seguridad en Red (SG vs NACL)]]** y **[[Tablas de Enrutamiento]]**.
    * Identificación: **[[Direcciones IP (AWS)]]**.
* **[[Amazon Route 53]]**: El servicio de DNS (nombres de dominio).
* **[[Amazon CloudFront]]**: CDN para entregar contenido rápido cerca del usuario.

### 🛡️ Seguridad y Gestión
* **[[IAM (Identity Management Access)]]**: Gestión de usuarios, grupos y permisos. "Quién puede hacer qué".
* **[[Amazon CloudWatch]]**: Monitorización y observabilidad de toda la infraestructura.

## 3. Fundamentos Económicos
Entender cómo cobra AWS es vital para la certificación y la vida real.
* **[[Cloud - Fundamentos de Facturación y Costes]]**
* **[[Cloud - Fundamentos y Características]]**