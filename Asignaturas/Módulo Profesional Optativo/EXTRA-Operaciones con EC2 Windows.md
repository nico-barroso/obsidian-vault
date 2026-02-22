---
tags:
  - aws
  - ec2
  - windows
  - rdp
  - operaciones
---

| Concepto Clave | Nota Útil |
| :--- | :--- |
| **Protocolo** | **RDP** (Remote Desktop Protocol). |
| **Puerto** | TCP **3389**. |
| **Usuario Admin** | Por defecto suele ser `Administrator`. |
| **Herramienta** | "Conexión a Escritorio Remoto" (Windows) o "Microsoft Remote Desktop" (Mac). |

## 1. Proceso de Conexión (RDP)
A diferencia de Linux (que usa SSH y puerto 22), Windows requiere entorno gráfico.

### Requisitos de Red
* El **[[Security Groups]]** asociado a la instancia debe permitir tráfico entrante en el puerto **TCP 3389** desde tu IP.

### Obtención de la Contraseña (Decriptación)
AWS no te da la contraseña directamente; la genera y la cifra con tu Clave Pública.
1.  En la consola AWS: Seleccionar Instancia $\to$ Conectar $\to$ Cliente RDP.
2.  Clic en **"Obtener contraseña" (Get Password)**.
3.  **Descifrado:** Debes subir tu archivo de clave privada (`.pem`) que creaste al lanzar la instancia.
4.  AWS descifrará la cadena y te mostrará la contraseña de texto plano del usuario `Administrator`.



---

## 2. Gestión de Almacenamiento (Añadir EBS)
Cuando adjuntas un volumen [[EBS]] extra a una instancia Windows desde la consola de AWS, **no aparece automáticamente** disponible para guardar archivos. Debes configurarlo dentro del S.O.

### Paso a paso:
1.  **En AWS Console:** Crear volumen y adjuntar (Attach) a la instancia (recordar: misma AZ).
2.  **En Windows (RDP):**
    * Abrir la herramienta **Administración de discos** (Ejecutar `diskmgmt.msc`).
    * Verás el disco como "Offline" o "Desconocido".
3.  **Activación:**
    * Clic derecho $\to$ **En línea** (Online).
    * Clic derecho $\to$ **Inicializar disco** (MBR o GPT).
    * Clic derecho en el espacio no asignado $\to$ **Nuevo volumen simple** (Asignar letra y formatear en NTFS).



> **Nota:** Si no haces esto, el disco existe físicamente, pero Windows no lo "ve" en el Explorador de Archivos.