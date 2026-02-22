
Un **Internet Gateway** es un componente lógico, escalable horizontalmente, redundante y de alta disponibilidad que permite la comunicación entre tu VPC e Internet.

- **Sin él:** Tu VPC es una "caja cerrada". Nadie entra, nadie sale.
    
- **Con él:** Abres una puerta para el tráfico entrante y saliente.
    
- **Rendimiento:** Al ser un objeto lógico gestionado por AWS, **no impone riesgos de disponibilidad ni restricciones de ancho de banda**. No es un aparato físico que se pueda "saturar" como un router casero.
    

### 2. Sus dos funciones principales

1. **Dar acceso:** Proporciona un objetivo (target) en tus tablas de enrutamiento para el tráfico que se dirige a internet.
    
2. **Traducción de Direcciones (NAT 1 a 1):** Realiza la traducción de direcciones de red para las instancias que tienen direcciones IP públicas asignadas (IPv4).
    

> **Analogía:** Imagina que tu VPC es un edificio de oficinas muy seguro (Intranet). El **Internet Gateway** es la **Puerta Principal** que da a la calle. Sin esa puerta, los empleados (servidores) no pueden salir a comprar comida (descargar actualizaciones) ni los clientes pueden entrar al vestíbulo (ver tu web).

### 3. ¿Cómo habilitar el acceso a Internet? (Pasos de Configuración)

Para que una subred sea realmente pública, debes seguir estos pasos religiosamente:

1. **Crear el IGW:** En la consola de AWS.
    
2. **Adjuntar (Attach):** Conectar el IGW a tu VPC.
    
    - _Ojo:_ Solo puedes adjuntar **UN** IGW por VPC.
        
3. **Configurar la Ruta:** Ir a la _Route Table_ de tu subred y añadir:
    
    - **Destination:** `0.0.0.0/0` (Todo el tráfico de internet).
        
    - **Target:** `igw-xxxxxxxx` (El ID de tu Internet Gateway).
        
4. **Revisar ACLs y Security Groups:** Asegurarte de que no haya reglas de firewall bloqueando el tráfico.
    

### 4. Diferencia Vital: IGW vs. NAT Gateway

Esta es una confusión clásica. Ambos sirven para "salir" a internet, pero con matices distintos:

|**Característica**|**Internet Gateway (IGW)**|**NAT Gateway**|
|---|---|---|
|**Ubicación**|Se adjunta al borde de la VPC.|Vive dentro de una Subred Pública.|
|**Dirección del tráfico**|**Bidireccional** (Entrada y Salida).|**Unidireccional** (Solo Salida).|
|**Uso Principal**|Para servidores Web (Subredes Públicas) que necesitan ser visitados por usuarios.|Para bases de datos (Subredes Privadas) que necesitan bajar parches pero **NO** deben ser accesibles desde fuera.|
|**Coste**|Gratuito (solo pagas la transferencia de datos).|Se paga por hora + procesamiento de datos.|

---

### 💡 AWS Exam Tip

Si en el examen te preguntan: "¿Por qué mi instancia EC2 en una subred pública no tiene internet si ya tiene una IP pública?"

Casi siempre la respuesta es: "Falta la ruta hacia el Internet Gateway en la Tabla de Enrutamiento" o "El Internet Gateway no está adjuntado a la VPC".