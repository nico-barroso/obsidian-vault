### 1. Definición y Concepto

Una **VPC** es una sección aislada lógicamente de la nube de AWS que te permite controlar tu entorno de red virtual.

- **¿Es un enrutamiento?** No exactamente. La VPC es el **"contenedor"** o la casa donde viven tus recursos. El enrutamiento (Route Tables) es el sistema de pasillos y puertas dentro de esa casa.
    
- **Alcance:** Una VPC pertenece a una **ÚNICA REGIÓN** (ej. `us-east-1`). No puede extenderse entre regiones.
    
- **VPC Default:** Al crear una cuenta, AWS crea una "VPC predeterminada" en cada región automáticamente para que puedas lanzar servidores (EC2) de inmediato. Es un servicio **gratuito** (solo pagas por los recursos que lanzas dentro, como las EC2).
    

	[[Tablas de Enrutamiento]]
> **⚠️ Aclaración importante sobre servicios:**
> 
> - **Viven DENTRO de la VPC:** Instancias [[EC2]], Bases de datos RDS, Lambda (opcionalmente). Tienen IP privada dentro de tu red.
>     
> - **Viven FUERA de la VPC (pero se conectan):** [[Amazon S3]] y DynamoDB. Son servicios públicos regionales. Para conectarlos de forma privada se usan _VPC Endpoints_, pero técnicamente no están "dentro" de una subred.
>     

---

### 2. Subredes (Subnets)

Como una VPC puede ser muy grande, la dividimos en trozos más pequeños llamados subredes.

- **Definición:** Un intervalo de direcciones IP que divide una VPC.
    
- **Regla de Oro:** Una subred pertenece a una **ÚNICA ZONA DE DISPONIBILIDAD (AZ)**.
    
    - _Nota:_ Una VPC abarca toda la región, pero la subred está confinada a un Data Center (AZ).
        

#### Clasificación: Pública vs. Privada

La diferencia NO es la seguridad (ambas son seguras), sino la **conectividad a Internet**.

- **Subred Pública:** Tiene una ruta directa a un **Internet Gateway (IGW)**. Puede "salir" a internet y recibir tráfico de internet.
    
- **Subred Privada:** NO tiene ruta al Internet Gateway. Los recursos aquí no pueden ser alcanzados directamente desde fuera.
    

---

### 3. Ejemplos de Arquitectura: ¿Qué pongo dónde?

Aquí tienes el ejemplo práctico para tu aplicación (App Web + Base de Datos):

|Tipo de Subred|Qué servicios colocar aquí|Por qué|
|---|---|---|
|**🌐 Subred Pública**|**Load Balancer (ALB):** Para recibir el tráfico de los usuarios. <br><br>  <br><br>**NAT Gateway:** Para que las máquinas privadas puedan descargar actualizaciones. <br><br>  <br><br>**Bastion Host:** Servidor "puente" para que tú te conectes a administrar.|Necesitan hablar directamente con Internet (entrada o salida).|
|**🔒 Subred Privada**|**Web Server / Backend (EC2):** Donde corre tu código Java/Node. <br><br>  <br><br>**Base de Datos (RDS/SQL):** Donde guardas los datos. <br><br>  <br><br>**Caché (ElastiCache):** Datos temporales.|Por seguridad. Nadie debe poder hacer "ping" a tu base de datos desde su casa. Solo el Load Balancer (público) puede hablar con el Backend (privado).|

Exportar a Hojas de cálculo

---

### 4. Tablas de Enrutamiento (Route Tables)

Son el mapa GPS de tu red. Contienen un conjunto de reglas (rutas) para dirigir el tráfico.

- **Componentes:**
    
    - **Destino (Destination):** ¿A dónde quiere ir el paquete? (ej. `0.0.0.0/0` significa "a cualquier sitio de internet").
        
    - **Objetivo (Target):** ¿A través de quién lo envío? (ej. `Internet Gateway`).
        

#### Ejemplo de Configuración Real

Imagina que configuras la red para tu App:

**A. Tabla de la Subred PÚBLICA** Queremos que salga a internet directamente. | Destination | Target | Explicación | | :--- | :--- | :--- | | `10.0.0.0/16` | `Local` | Permite hablar con otras máquinas dentro de la VPC. | | `0.0.0.0/0` | **`Internet Gateway (IGW)`** | Todo lo que no sea local, mándalo a Internet. |

**B. Tabla de la Subred PRIVADA** Queremos que la base de datos esté segura, pero que pueda descargar parches de seguridad (salida sí, entrada no). | Destination | Target | Explicación | | :--- | :--- | :--- | | `10.0.0.0/16` | `Local` | Permite hablar con el Backend o el Load Balancer. | | `0.0.0.0/0` | **`NAT Gateway`** | Manda el tráfico a internet a través del intermediario (NAT) que está en la pública. |

---

### 💡 Tip para el Examen

Si te preguntan: _"¿Cómo hago que una subred sea pública?"_ La respuesta técnica es: **"Asociándole una Tabla de Enrutamiento que tenga una ruta hacia el Internet Gateway (IGW)".**