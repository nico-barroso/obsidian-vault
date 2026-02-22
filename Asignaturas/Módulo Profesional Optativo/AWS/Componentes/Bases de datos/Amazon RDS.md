---
tags:
  - aws
  - base-de-datos
  - rds
  - sql
  - alta-disponibilidad
---

| Concepto Clave | Nota Útil                                                                       |
| :------------- | :------------------------------------------------------------------------------ |
| **Definición** | Servicio de base de datos relacional **gestionado**.                            |
| **Ventaja**    | Automatiza tareas administrativas (Backups, Parches, Escalado).                 |
| **Motores**    | Soporta 6 motores: Aurora, MySQL, MariaDB, PostgreSQL, Oracle, SQL Server.      |
| **Ubicación**  | Siempre debe desplegarse en una **Subred Privada** dentro de la [[Amazon VPC]]. |

## 1. ¿Por qué usar RDS? (El problema de la gestión)
El desafío de las bases de datos tradicionales es el mantenimiento ("Heavy Lifting").

* **On-Premise:** Gestionas hardware, energía, refrigeración, S.O., parches y backups físicos.
* **En [[EC2]] (IaaS):** Te ahorras el hardware, pero sigues gestionando el S.O., los parches de la base de datos, la configuración de replicación y las copias de seguridad manuales.
* **En RDS (Gestionado):** AWS se encarga de:
    * Aprovisionamiento de infraestructura.
    * Instalación y parches del S.O. y motor de base de datos.
    * Copias de seguridad automáticas.
    * Alta disponibilidad (con Multi-AZ).



## 2. Motores Compatibles
RDS no es una base de datos en sí, es el servicio que aloja estos motores:
1.  **Amazon Aurora** (Propio de AWS, compatible con MySQL/PostgreSQL).
2.  PostgreSQL.
3.  MySQL.
4.  MariaDB.
5.  Oracle.
6.  Microsoft SQL Server.

## 3. Arquitecturas de Disponibilidad y Rendimiento
Es vital distinguir entre "No perder datos" (Multi-AZ) y "Mejorar velocidad" (Read Replicas).

### A. Implementación Multi-AZ (Alta Disponibilidad)
* **Objetivo:** **Disaster Recovery** (Si falla una, sigue la otra).
* **Funcionamiento:** Crea una réplica exacta en una **Zona de Disponibilidad (AZ) diferente**.
* **Sincronización:** **Síncrona** (El dato se escribe en ambas a la vez).
* **Uso:** Si la instancia principal cae, AWS cambia el DNS automáticamente a la réplica (Failover). **No sirve para mejorar rendimiento**, la réplica está "dormida" esperando un fallo.



### B. Réplicas de Lectura (Read Replicas)
* **Objetivo:** **Rendimiento y Escalado** (Aliviar carga).
* **Funcionamiento:** Crea copias de solo lectura de la base de datos maestra.
* **Sincronización:** **Asíncrona** (Puede haber un milisegundo de retraso).
* **¿Para qué se usa? **
    * Imagina una web de noticias. Hay 1 editor escribiendo (Insert/Update) y 1 millón de usuarios leyendo (Select).
    * El editor escribe en la **RDS Principal**.
    * El millón de usuarios leen de las **Réplicas de Lectura**.
    * *Resultado:* La base de datos principal no se satura y la web va rápida.



## 4. Redes y Seguridad
Aunque es un servicio gestionado, RDS utiliza instancias por debajo.
*[[Amazon VPC]]:** Se despliega dentro de tu red virtual.
* **Subredes:** Best Practice $\to$ Usar **Subredes Privadas** (sin acceso directo a internet) para proteger los datos.
* **Security Groups:** Controlan quién puede conectarse al puerto de la base de datos (ej. Puerto 3306 para MySQL).

## 5. Facturación
Se paga un extra respecto a [[EC2]] por la gestión automatizada.
* **Factores:** Motor de base de datos, Tamaño de la instancia (CPU/RAM) y Almacenamiento provisionado.
* **Modelos de compra:**
    * **On-Demand:** Pago por hora.
    * **Reserved Instances:** Compromiso de 1 o 3 años (descuento significativo).