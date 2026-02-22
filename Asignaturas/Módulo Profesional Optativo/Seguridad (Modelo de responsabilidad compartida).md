La seguridad y el cåumplimiento en AWS son una responsabilidad compartida entre el proveedor y el cliente. Esta diferenciación es crucial para saber a quién "culpar" (o quién debe actuar) ante un problema.

### 1. La Regla de Oro

- **AWS** es responsable de la seguridad **DE** la nube.
    
- **El Cliente (Tú)** eres responsable de la seguridad **EN** la nube.


---

### 2. Responsabilidades de AWS (Seguridad DE la nube)

AWS protege la infraestructura global que ejecuta todos los servicios. Tú no tienes acceso a esto, por lo que ellos deben asegurarlo.

- **Infraestructura Física:** Seguridad de los Centros de Datos (cámaras, guardias, control de acceso biométrico). Nadie entra ahí, ni siquiera tú.
    
- **Hardware:** Servidores, dispositivos de almacenamiento y generadores de energía.
    
- **Red Global:** El cableado físico, routers y la red troncal (backbone) que conecta las regiones.
    
- **Virtualización:** La capa de software (Hypervisor) que separa unas máquinas virtuales de otras (asegura que tu vecino en la nube no pueda ver tus datos).
    

---

### 3. Responsabilidades del Cliente (Seguridad EN la nube)

Tú eres responsable de todo lo que "pones" dentro de la nube. AWS te da la puerta blindada (infraestructura), pero tú decides si la dejas abierta o a quién le das la llave.

- **Datos del Cliente:** Eres dueño de tus datos. Tú decides si los cifras (encriptas) o no.
    
- **Plataformas y Aplicaciones:** Gestión de tu código y software instalado.
    
- **Sistema Operativo (en IaaS):** Actualizaciones y parches de seguridad (ej. Windows Update en una EC2).
    
- **Configuración de Red:** Configuración del Firewall (Security Groups), control de tráfico y acceso a puertos.
    
- **Gestión de Identidad (IAM):** Decidir quién tiene usuario y contraseña, y qué permisos tiene.
    

---

### 4. Ejemplos Prácticos: ¿Quién es responsable?

Aquí tienes la tabla de ejemplos que pedías para visualizarlo mejor:

|Escenario de Seguridad|Responsable|¿Por qué?|
|---|---|---|
|**Un disco duro falla físicamente**|🟠 **AWS**|Es parte de la infraestructura física del Data Center.|
|**Roban la contraseña de un empleado**|🔵 **Cliente**|La gestión de usuarios (IAM) y políticas de contraseñas es tuya.|
|**Cae un rayo en el Data Center**|🟠 **AWS**|Seguridad física y continuidad del edificio.|
|**Hacker entra por un puerto abierto**|🔵 **Cliente**|Tú configuras el Firewall (Security Group) de tu instancia.|
|**Actualizar el Windows de tu servidor**|🔵 **Cliente**|En IaaS (EC2), el S.O. es responsabilidad tuya.|
|**Aislar tu máquina de otros clientes**|🟠 **AWS**|La virtualización base la garantiza AWS.|
|**Encriptar la base de datos**|🔵 **Cliente**|AWS te da la herramienta, pero tú debes activarla.|

Exportar a Hojas de cálculo

---

### 5. IAM (Identity and Access Management)

Es el servicio "portero" de tu cuenta. Permite controlar el acceso a los recursos de AWS de forma segura.

- **Definición:** Servicio que gestiona el "Quién" (Autenticación) y el "Qué puede hacer" (Autorización).
    
- **Principio de Privilegio Mínimo (Least Privilege):** Regla de oro en seguridad. Solo dar el acceso _mínimo necesario_ para realizar una tarea.
    
    - _Ejemplo:_ Si Nico solo necesita leer archivos de S3, no le des permisos de Administrador ("AdministratorAccess").
        
- **Componentes:**
    
    - **Users:** Personas o servicios.
        
    - **Groups:** Conjunto de usuarios con permisos similares (ej. "Developers").
        
    - **Roles:** Permisos temporales para máquinas o servicios (ej. que una EC2 pueda escribir en S3).
        
    - **Policies:** Documentos JSON donde se escriben las reglas de permiso.
        

---

### 💡 Nota importante sobre el Modelo

La responsabilidad del cliente **varía** según el servicio:

- En **EC2 (IaaS)**: Tienes MUCHA responsabilidad (parchear el SO).
    
- En **S3 o DynamoDB (Servicios gestionados)**: Tienes MENOS responsabilidad (AWS gestiona el SO y parches, tú solo los datos y el acceso).