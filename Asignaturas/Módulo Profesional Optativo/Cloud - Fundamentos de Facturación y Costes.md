
| Concepto Clave   | Nota Útil                                                         |
| :--------------- | :---------------------------------------------------------------- |
| **Modelo**       | Pago por uso (Pay-as-you-go). Gasto Operativo ([[OpEx]]).         |
| **Regla de Oro** | "Entrar es gratis, salir cuesta dinero" (Transferencia de datos). |
| **Ámbito**       | [[Cloud Computing]] / [[Amazon Web Services (AWS)]]               |

## 1. Los 3 Pilares del Coste
Aunque cada proveedor tiene particularidades, la factura se basa en tres variables principales:

### A. Cómputo (Compute)
Pagas por **capacidad de procesamiento** (CPU/RAM) durante un tiempo determinado.
* **Unidad:** Por hora o por segundo (depende del SO y proveedor).
* **Variabilidad:** El precio cambia según el tamaño y tipo de instancia (ej. `t3.micro` vs `c5.large` en [[EC2]]).

### B. Almacenamiento (Storage)
Pagas por el **espacio consumido** en disco o en objetos.
* **Unidad:** Generalmente **GB/mes**.
* **Matiz:** El coste varía según la "clase" de almacenamiento (acceso frecuente es más caro que el archivado en frío o *Cold Storage*).

### C. Transferencia de Datos (Data Transfer)
* **Inbound (Entrada):** Generalmente **GRATUITA**. Los proveedores incentivan la subida de datos a la nube.
* **Outbound (Salida):** Se cobra por GB transferido hacia Internet u otras regiones. Es un coste crítico a vigilar.

[Image of cloud data transfer cost inbound outbound]

---

## 2. Estrategias de Ahorro
Por defecto, el precio es **On-Demand** (bajo demanda), que ofrece máxima flexibilidad pero es el más caro.

![[Instancias reservadas]]
---

## 3. Herramientas de Gestión de Costes (AWS)
Diferenciación clave para examen y certificación:

| Herramienta | Cuándo se usa | Función Principal |
| :--- | :--- | :--- |
| **AWS Pricing Calculator** | **ANTES** del despliegue | Simular arquitecturas y **estimar** costes mensuales. Comparar precios entre regiones. |
| **AWS Cost Explorer** | **DESPUÉS/DURANTE** | Visualizar y analizar costes **pasados** o actuales con gráficos. |
| **AWS Budgets** | **SIEMPRE** | Configurar **alertas** si el coste o uso supera un límite definido. Evita el *Bill Shock*. |

> **Nota:** La primera factura real sirve como "Línea Base" (Baseline) para ajustar las previsiones de las calculadoras.