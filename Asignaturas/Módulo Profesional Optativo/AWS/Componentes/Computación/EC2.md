---
tags:
  - aws
  - compute
  - ec2
  - iaas
---


| Concepto Clave | Nota Útil                                                                   |
| :------------- | :-------------------------------------------------------------------------- |
| **Definición** | Servicio web de capacidad informática redimensionable (máquinas virtuales). |
| **Modelo**     | [[IaaS]] (Infraestructura como Servicio).                                   |
| **Acceso**     | Vía Terminal (**SSH** para Linux) o **RDP** (para Windows).                 |
| **Control**    | Absoluto (Root/Admin). Tú gestionas el S.O.                                 |

## Definición y Propósito
**Amazon EC2** (Elastic Cloud Computing) permite alquilar servidores virtuales (**Instancias**) eliminando la necesidad de hardware físico.
* **Abstracción:** AWS gestiona el "hierro" (host físico); tú gestionas el Sistema Operativo invitado.
* **Elasticidad:** Capacidad de escalar (aumentar/disminuir recursos) en minutos.



## 1. Tipos de Instancias (Categorías)
AWS agrupa las instancias según su especialización en hardware:

* **General Purpose (Propósito General - Familia T, M):** Equilibrio entre cómputo, memoria y redes. (Ej. Servidores web, repositorios).
* **Compute Optimized (Optimizado para Cómputo - Familia C):** Alto rendimiento de procesador. (Ej. Procesamiento por lotes, codificación de vídeo).
* **Memory Optimized (Optimizado para Memoria - Familia R, X):** Para cargas que procesan grandes datos en memoria. (Ej. Bases de datos en tiempo real).
* **Storage Optimized (Optimizado para Almacenamiento - Familia I, D):** Alto I/O de disco. (Ej. Big Data, NoSQL).
* **Accelerated Computing (Aceleración - Familia P, G):** Usan GPUs. (Ej. Machine Learning, Gráficos).

## 2. Almacenamiento en EC2
Una instancia puede conectarse a varios tipos de almacenamiento:

| Tipo                                                    | Descripción                                                           | Persistencia                                                                        |
| :------------------------------------------------------ | :-------------------------------------------------------------------- | :---------------------------------------------------------------------------------- |
| **[[EBS (Elastic Block Store)]] (Elastic Block Store)** | El "disco duro" estándar. Volúmenes creados a partir de instantáneas. | **Persistente** (los datos siguen ahí si paras la instancia y los siguen cobrando). |
| **Instance Store**                                      | Disco físico pegado al host. Muy rápido pero volátil.                 | **Efímero** (si paras la instancia, pierdes los datos).                             |
| **[[EFS]] (Elastic File System)**                       | Sistema de archivos compartido para Linux.                            | Persistente y compartido entre muchas EC2.                                          |
| **[[Amazon S3]]**                                              | Almacenamiento de objetos.                                            | Se accede vía API/Internet, no como disco local.                                    |



## 3. Seguridad en EC2
La seguridad se aplica en capas:

* **Key Pairs (Par de Claves):** Necesarias para el login inicial.
    * *Clave Privada (.pem/.ppk):* La guardas tú.
    * *Clave Pública:* La guarda AWS en la instancia.
* **[[Security Groups]] (Grupos de Seguridad):** Firewall virtual a nivel de instancia. Controla puertos y protocolos (ej. abrir puerto 80 para web, 22 para SSH).
* **IAM Roles:** Se adjuntan a la instancia para darle permisos.
    * *Best Practice:* En lugar de guardar credenciales de AWS (Access Keys) dentro del código en la instancia, asignas un **Rol** a la máquina para que pueda acceder a otros servicios (como S3 o DynamoDB) de forma segura.

## 4. Redes e IP
Comportamiento de las direcciones IP en [[EC2]]:

* **IP Privada:** Fija. Se usa para comunicación interna en la nube.
* **IP Pública (Dinámica):** Por defecto, si apagas (*Stop*) y enciendes (*Start*) la máquina, la IP pública **CAMBIA**.
* **Elastic IP (IP Elástica):**
    * Es una **IP Pública Estática** (fija).
    * Se debe asignar manualmente.
    * *Coste:* Es gratis si está en uso. AWS cobra si la reservas y **no la usas** (para evitar que acapares direcciones).
>    **Es interesante para cuando tengas tu propio servidor y no tener que cambiarla y apuntar al mismo permitiendo filtrar accesos con IP,**

## 5. Gestión
* **Etiquetas (Tags):** Metadatos clave-valor (ej. `Proyecto: WebApp`, `Entorno: Producción`) fundamentales para organizar recursos y controlar costes.