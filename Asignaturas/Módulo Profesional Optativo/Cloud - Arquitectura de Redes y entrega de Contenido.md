

| **Concepto Clave** | **Nota Útil**                                                                                        |
| ------------------ | ---------------------------------------------------------------------------------------------------- |
| **Amazon VPC**     | Red virtual aislada lógicamente en la nube de AWS.                                                   |
| **Alcance**        | Regional (vive en una única [[AWS - Regiones y Avaialbilty Zones (AZ)]]), pero abarca múltiples AZs. |
| **Aislamiento**    | Permite control total sobre el entorno de red (IPs, subredes, enrutamiento).                         |
|                    |                                                                                                      |

#### 1. [[Amazon VPC]] (Virtual Private Cloud)

- **Concepto:** Es el contenedor principal. Un entorno de red privado y aislado donde despliegas tus recursos.
    
- **Función:** Define los límites lógicos de tu infraestructura. Nada entra ni sale sin configuración explícita.
    
- **Jerarquía:** Pertenece a una sola Región.
    

#### 2. Direccionamiento: IP y CIDR

- **CIDR Block:** Rango de direcciones IP privadas asignadas al crear la VPC (ej. `10.0.0.0/16`). Es el espacio total disponible.
    
- **Subredes (Subnets):** Segmentación del bloque CIDR principal en bloques más pequeños.
    
    - Permiten organizar recursos por funcionalidad o seguridad.
        
    - Se asocian a una zona de disponibilidad específica.
        
    - Enlace relacionado: [[Direcciones IP en AWS]]
        

#### 3. Route Tables (Tablas de Enrutamiento)

- **Función:** Actúan como el "cerebro" lógico del tráfico. Cada subred tiene una tabla asociada.
    
- **Mecanismo:** Contiene reglas (rutas) que determinan hacia dónde se dirige cada paquete de datos.
    
    - **Ruta Local:** Permite la comunicación entre instancias dentro de la misma VPC.
        
    - **Ruta Externa:** Dirige el tráfico hacia internet (vía IGW) u otras redes.
        

#### 4. Internet Gateway (IGW)

- **Concepto:** Componente horizontalmente escalable y redundante.
    
- **Función:** Habilita la comunicación entre las instancias de tu VPC e Internet.
    
- **Requisito:** Sin un IGW adjunto y una ruta en la Route Table apuntando a él, la subred es privada (sin acceso directo a internet).
    

---

### Esquema Mental (Analogía)

Esta tabla resume la relación entre componentes físicos y componentes Cloud.

|**Concepto Físico**|**Concepto AWS**|**Función**|
|---|---|---|
|**La Oficina / Red Local**|**VPC**|El espacio seguro y delimitado donde residen los recursos.|
|**Los Departamentos**|**Subredes**|Divisiones organizativas dentro de la red (RRHH, Frontend...).|
|**El Guardia de Seguridad**|**Route Table**|Verifica el destino del tráfico y dirige el camino.|
|**La Puerta Principal**|**Internet Gateway (IGW)**|El punto de salida hacia el exterior (Internet).|
|**Número de Teléfono**|**IP Address**|Identificador único para localizar un recurso.|

---

### Metadatos y Organización

**Lista de enlaces sugeridos:**

- [[AWS - Regiones y Avaialbilty Zones (AZ)]]
    
- [[AWS - Subredes Públicas vs Privadas]]
    
- [[AWS - Seguridad en Red (SG vs NACL)]]


Tags recomendados:

#aws #cloud #networking #vpc #sistemas #infraestructura

---
