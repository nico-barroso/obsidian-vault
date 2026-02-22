---
tags:
  - aws
  - ebs
  - almacenamiento
  - infraestructura
---

| Concepto Clave | Nota Útil |
| :--- | :--- |
| **Definición** | Almacenamiento en bloque persistente para usar con [[EC2]]. |
| **Naturaleza** | Es un disco de **RED**, no está conectado físicamente al servidor. |
| **Disponibilidad** | **Zonal**. Un volumen vive en una sola AZ (Availability Zone). |
| **Seguridad** | Soporta cifrado AES-256 (Datos en reposo y en tránsito). |

## Definición y Concepto
**Amazon EBS** (Elastic Block Store) actúa como un disco duro virtual de alto rendimiento.
* Se conecta a la instancia a través de la red.
* Permite persistencia de datos: si detienes (*Stop*) la instancia, los datos **no se pierden**.
* Es escalable: puedes aumentar el tamaño o cambiar el tipo de volumen sobre la marcha (live configuration change).



## 1. Tipos de Volúmenes (Familia de Discos)
Elegir el tipo correcto determina el coste y el rendimiento. Se divide en SSD (Rendimiento) y HDD (Capacidad).

| Categoría | Tipo | Nombre | Caso de Uso Ideal |
| :--- | :--- | :--- | :--- |
| **SSD** | **General Purpose** | `gp2`, `gp3` | **El estándar.** Balanza precio/rendimiento. Desktops, entornos de desarrollo, webs. |
| **SSD** | **Provisioned IOPS** | `io1`, `io2` | **Misión Crítica.** Bases de datos grandes (Oracle, SQL Server) que necesitan IOPS garantizados y latencia sub-milisegundo. |
| **HDD** | **Throughput Optimized** | `st1` | **Big Data.** Data warehouses, log processing. Optimizado para lectura secuencial grande. No sirve para arranque (boot). |
| **HDD** | **Cold HDD** | `sc1` | **Archivos.** Datos de acceso infrecuente. El coste más bajo. No sirve para arranque. |



## 2. Snapshots (Instantáneas)
Son las copias de seguridad (backups) de los volúmenes EBS.
* **Almacenamiento:** Se guardan técnicamente en [[Amazon S3]] (aunque no los ves en tu bucket, los gestiona AWS).
* **Incrementales:** Solo se copian los bloques que han cambiado desde la última foto. Esto ahorra espacio y dinero.
* **Uso:** Sirven para crear nuevos volúmenes o crear [[Amazon Machine Image (AMI)]].

## 3. Limitación de Zona (El problema de la AZ)
**Regla:** Un volumen EBS en `us-east-1a` **NO** se puede adjuntar a una instancia en `us-east-1b`.

**Solución para mover datos:**
1.  Hacer un **Snapshot** del volumen en la Zona A.
2.  Copiar el Snapshot (si es a otra región) o usarlo directamente.
3.  Crear un **nuevo volumen** a partir del Snapshot especificando la Zona B.

## 4. Delete on Termination (Borrado al Terminar)
Es una configuración ("flag") de la instancia EC2:
* **Root Volume (Raíz):** Por defecto, se **BORRA** cuando terminas la instancia.
* **Data Volume (Datos extra):** Por defecto, se **CONSERVA** (se queda huérfano) cuando terminas la instancia.
* *Nota:* Esto se puede cambiar al lanzar la instancia para evitar borrar datos accidentales.