
Una **Tabla de Enrutamiento** es un conjunto de reglas (llamadas _rutas_) que determinan hacia dónde se dirige el tráfico de red proveniente de tu subred o puerta de enlace.

> **La mejor analogía:** Piensa en la Route Table como el **GPS** o el **Controlador de Tráfico** de cada subred. Cuando un paquete de datos sale de tu servidor, le pregunta a la tabla: _"Quiero ir a la IP 8.8.8.8, ¿por dónde salgo?"_. La tabla mira sus reglas y le dice: _"Sal por la puerta del Internet Gateway"_.

### 2. Anatomía de una Ruta

Cada regla en la tabla tiene dos componentes fundamentales que debes memorizar:

- **Destino (Destination):** ¿A DÓNDE quiere ir el paquete?
    
    - Se expresa en formato CIDR (ej. `10.0.0.0/16` o `0.0.0.0/0`).
        
    - Es el "rango de direcciones IP" al que intentas llegar.
        
- **Objetivo (Target):** ¿A TRAVÉS DE QUÉ recurso lo envío?
    
    - Es la "puerta" o el medio de transporte.
        
    - Ejemplos: `local`, `internet-gateway`, `nat-gateway`, `virtual-private-gateway`.
        

---

### 3. La Regla "Local" (Implícita)

Siempre que creas una [[Amazon VPC]], AWS añade automáticamente una regla que **NO se puede borrar**.

- **Destination:** El rango de tu VPC (ej. `10.0.0.0/16`).
    
- **Target:** `Local`.
    
- **Significado:** "Cualquier máquina dentro de esta VPC puede hablar con cualquier otra máquina de la VPC directamente". Esto permite que tu Backend hable con tu Base de Datos sin salir a internet.
    

---

### 4. Funcionamiento Práctico: El Algoritmo de Decisión

Cuando hay varias rutas, ¿cuál elige AWS?

Criterio: AWS siempre usa la ruta más específica (la que coincida con el rango CIDR más pequeño/preciso).

#### Ejemplo de Prioridad:

Imagina que quieres enviar un paquete a la IP `10.0.1.50`.

1. Ruta A (`10.0.0.0/16` -> Local): Coincide.
    
2. Ruta B (`0.0.0.0/0` -> [[Internet Gateway (IGW)]]): Coincide (porque abarca todo).
    

**Resultado:** Gana la **Ruta A** porque es más específica (`/16` es más preciso que `/0`). El tráfico se queda dentro de la red local y no sale a internet.

---

### 5. Asociación con Subredes (Subnet Association)

Este concepto es vital para el examen y la arquitectura real:

1. **Cada subred DEBE estar asociada a una tabla de enrutamiento.**
    
2. **Relación 1 a N:** Una tabla de enrutamiento puede asociarse a _muchas_ subredes a la vez.
    
3. **Exclusividad:** Una subred solo puede tener _una_ tabla de enrutamiento activa a la vez.
    
4. **Main Route Table:** Si no asocias una subred explícitamente a una tabla personalizada, AWS la asocia automáticamente a la "Tabla Principal" (Main). _Consejo:_ Evita usar la Main para todo; crea tablas personalizadas para tener control granular.
    

---

### 6. Ejemplo de Configuración: Pública vs. Privada

Así es como se configuran las tablas para separar los ambientes en tu proyecto:

#### 🟢 Tabla de Rutas PÚBLICA (Public Route Table)

Asociada a subredes donde viven Load Balancers o Servidores Web.

|**Destination**|**Target**|**¿Qué hace?**|
|---|---|---|
|`10.0.0.0/16`|`Local`|Permite tráfico interno entre servidores.|
|**`0.0.0.0/0`**|**`igw-xxxxxx`**|**La clave:** Todo el tráfico que no sea local, mándalo al Internet Gateway. Esto hace que la subred sea "Pública".|

#### 🔒 Tabla de Rutas PRIVADA (Private Route Table)

Asociada a subredes de Bases de Datos o Backend seguros.

|**Destination**|**Target**|**¿Qué hace?**|
|---|---|---|
|`10.0.0.0/16`|`Local`|Permite tráfico interno.|
|**`0.0.0.0/0`**|**`nat-xxxxxx`**|Todo el tráfico de salida (ej. actualizaciones) se manda al NAT Gateway. **NO** permite entrada desde internet.|

---

### 💡 AWS Exam Tip (Developer Associate)

Si te preguntan: _"He creado un Internet Gateway y lo he adjuntado a la VPC, pero mis instancias siguen sin poder salir a Internet. ¿Qué falta?"_

La respuesta es casi siempre: **Actualizar la Tabla de Enrutamiento**. El hardware (IGW) puede estar ahí, pero si el GPS (Route Table) no tiene la regla `0.0.0.0/0 -> igw-id`, el tráfico no sabrá cómo llegar a la puerta.