---
tags:
  - aws
  - ami
  - ec2
  - virtualizacion
---


| Concepto Clave | Nota Útil |
| :--- | :--- |
| **Definición** | Plantilla necesaria para lanzar una instancia [[EC2]]. |
| **Contenido** | Sistema Operativo + Software preinstalado + Configuración. |
| **Analogía** | Es como una "Imagen ISO" o un "Ghost" de un disco duro. |
| **Ámbito** | Específico de una **Región** (si quieres usarla en otra, debes copiarla). |

## Definición
Una **Amazon Machine Image (AMI)** es una plantilla maestra que contiene la configuración de software (sistema operativo, servidor de aplicaciones y aplicaciones) necesaria para iniciar una instancia.

**Regla de oro:** Puedes lanzar múltiples instancias desde una sola AMI cuando necesites múltiples servidores con la misma configuración.



## Ciclo de Vida Típico
1.  Lanzas una instancia base desde una AMI pública (ej. Ubuntu Linux).
2.  Te conectas, actualizas el sistema e instalas tu aplicación (ej. Apache + PHP).
3.  Creas una **nueva AMI personalizada** a partir de esa instancia configurada.
4.  Ahora puedes lanzar nuevas instancias que ya tienen todo instalado y listo para funcionar (reduciendo tiempos de configuración).

## Fuentes de AMIs (¿De dónde las saco?)
Al lanzar una instancia, debes elegir una fuente:

1.  **Quick Start (Inicio Rápido):** AMIs oficiales mantenidas por AWS o partners (Amazon Linux 2, Ubuntu, Windows Server). Son las más seguras y usadas.
2.  **My AMIs (Mis AMIs):** Las imágenes privadas que tú has creado y guardado.
3.  **AWS Marketplace:** Catálogo digital donde vendedores externos venden su software empaquetado en AMIs (ej. un firewall Fortinet o una imagen endurecida de CIS). Pueden tener coste extra por licencia.
4.  **Community AMIs:** Imágenes compartidas públicamente por cualquiera. **Precaución:** Úsalas con cuidado, ya que el software que contienen no está verificado por AWS.

## Componentes de una AMI
Técnicamente, una AMI incluye:
* **Plantilla para el volumen raíz:** Define si el disco principal será [[EBS (Elastic Block Store)]] (persistente) o Instance Store (volátil).
* **Permisos de lanzamiento:** Controla qué cuentas de AWS pueden usar la AMI.
* **Mapeo de dispositivos de bloques:** Especifica qué volúmenes se adjuntan a la instancia al arrancar.