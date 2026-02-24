---
tags: [cloud, aws, networking, vpc]
category: Cloud
related: [[Cloud - Fundamentos y Características]]
---

# Arquitectura de Redes y Entrega de Contenido

| **Concepto Clave** | **Nota Útil** |
|---|---|
| **Amazon VPC** | Red virtual aislada lógicamente en AWS. |
| **Alcance** | Regional, múltiples AZs. |

## 1. VPC (Virtual Private Cloud)

Entorno de red privado y aislado. Define los límites lógicos.

- Pertenece a una sola Región.
- Control total sobre IPs, subredes, enrutamiento.

## 2. CIDR y Subredes

- **CIDR Block**: Rango de IPs privadas (ej. `10.0.0.0/16`)
- **Subredes**: Segmentación del CIDR, asociadas a una AZ

## 3. Route Tables

- "Cerebro" del tráfico
- Ruta Local: comunicación interna
- Ruta Externa: hacia internet (IGW)

## 4. Internet Gateway (IGW)

- Habilita comunicación entre VPC e Internet
- Sin IGW, la subred es privada

## Analogía

| Físico | AWS |
|---|---|
| Oficina | VPC |
| Departamentos | Subredes |
| Guardia seguridad | Route Table |
| Puerta principal | IGW |

> Ver: [[Cloud - Fundamentos y Características]]
