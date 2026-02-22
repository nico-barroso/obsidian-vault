---
sticker: emoji//1f61c
---

|**Concepto Clave**|**Nota Útil**|
|---|---|
|**Security Group (SG)**|Firewall virtual a nivel de **instancia**. Stateful (con memoria).|
|**Network ACL (NACL)**|Firewall a nivel de **subred**. Stateless (sin memoria).|
|**Defensa en Profundidad**|Se recomienda usar ambos para crear múltiples capas de seguridad.|

#### 1. Security Groups (Grupos de Seguridad)

Actúan como la última línea de defensa, protegiendo directamente la interfaz de red de la instancia (EC2, RDS, etc.).

- **Filosofía:** "Todo prohibido por defecto". Solo se definen reglas de acceso.
    
- **Reglas:** Solo admite **ALLOW** (Permitir). No es posible denegar explícitamente una IP.
    
- **Comportamiento: Stateful (Con Estado)**
    
    - Tienen memoria de las conexiones.
        
    - Si se permite el tráfico de **entrada** (Inbound), la respuesta de **salida** (Outbound) se permite **automáticamente**, independientemente de las reglas de salida.
        
    - _Analogía:_ Si el portero te deja entrar, asume que estás autorizado para salir.
        

#### 2. Network ACLs (Listas de Control de Acceso)

Actúan como una barrera perimetral para toda la subred. Todo el tráfico que entra o sale de la subred debe pasar por aquí antes de llegar a los Security Groups.

- **Filosofía:** Capa de seguridad opcional y "sin estado".
    
- **Reglas:** Admite **ALLOW** y **DENY**.
    
    - Permite bloquear IPs maliciosas específicas (función crítica que los SG no tienen).
        
    - **Orden:** Se evalúan numéricamente (la regla 100 prevalece sobre la 200). En cuanto una regla coincide, se detiene la evaluación.
        
- **Comportamiento: Stateless (Sin Estado)**
    
    - No recuerdan las conexiones.
        
    - Si permites tráfico de entrada (ej. puerto 80), **debes crear explícitamente** una regla de salida para permitir el retorno de los datos (normalmente hacia _ephemeral ports_ 1024-65535).
        
    - _Analogía:_ Control estricto; debes mostrar identificación tanto al entrar como al salir.
        

---

### Tabla Comparativa: SG vs NACL

|**Característica**|**Security Group (SG)**|**Network ACL (NACL)**|
|---|---|---|
|**Nivel de actuación**|Instancia (Interfaz de red)|Subred|
|**Tipo de Reglas**|Solo ALLOW|ALLOW y DENY|
|**Estado**|**Stateful** (Retorno automático)|**Stateless** (Retorno explícito)|
|**Evaluación**|Se evalúan todas las reglas|Orden numérico (se detiene al coincidir)|
|**Bloqueo de IPs**|No|Sí|

---

### Patrón de Diseño: "Security Group Chaining"

En arquitecturas de n capas, es una buena práctica referenciar **IDs de Security Groups** en lugar de IPs o rangos CIDR.

**Ejemplo de Arquitectura Web + Base de Datos:**

1. **SG-Web:**
    
    - Inbound: Puerto 80/443 desde `0.0.0.0/0` (Internet).
        
2. **SG-BaseDatos:**
    
    - Inbound: Puerto 3306 (MySQL).
        
    - **Source:** `sg-web-id` (En lugar de una IP).
        

**Ventaja:** Si el servidor web cambia de IP (por reinicio o auto-scaling), la base de datos sigue aceptando el tráfico automáticamente porque confía en el "grupo", no en la dirección IP.

---

### Metadatos y Organización

**Lista de enlaces sugeridos:**

- [[Cloud - Arquitectura de Redes y entrega de Contenido]] 
    
- [[AWS - Subredes Públicas vs Privadas]]
    
- [[Redes - Puertos y Protocolos Comunes]]
    

Tags recomendados:

#aws #seguridad #networking #firewall #best_practices #sistemas

---

Siguiente paso:

Con esto tienes cubierta la estructura y la seguridad básica. ¿Te gustaría que preparemos una nota sobre Almacenamiento (S3 vs EBS) o prefieres ver cómo conectar esta VPC con el exterior (NAT Gateway / Bastion Host)?