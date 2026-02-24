---
tags: [java, maven, build]
category: Programacion
related: [[Java]]
---

# POM (Project Object Model)

| **Concepto clave** | **Nota útil** |
| ------------------ | ------------- |
| **Siglas**         | **P**roject **O**bject **M**odel. |
| **Formato**        | XML. |
| **Función**        | Es el "DNI" y el "plano de construcción" del proyecto. |
| **Ubicación**      | Siempre en la raíz del proyecto. |

## 1. Coordenadas G.A.V.

- **GroupId**: Organización (dominio invertido). `com.miempresa.ventas`
- **ArtifactId**: Nombre del proyecto. `mi-api`
- **Version**: Estado del desarrollo. `1.0.0-SNAPSHOT`

## 2. Propiedades

Variables globales para evitar repetir versiones:

```xml
<properties>
    <java.version>17</java.version>
    <jackson.version>2.15.0</jackson.version>
</properties>
```

## 3. Dependencias

```xml
<dependencies>
    <dependency>
        <groupId>com.fasterxml.jackson.core</groupId>
        <artifactId>jackson-databind</artifactId>
        <version>${jackson.version}</version>
    </dependency>
</dependencies>
```

**Scope:**
- `compile`: Siempre necesaria
- `test`: Solo para tests
- `runtime`: Solo al ejecutar (ej. JDBC)

## 4. Build y Plugins

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.11.0</version>
        </plugin>
    </plugins>
</build>
```

> Ver: [[JDBC - Establecer Conexión|Conexión a BD]]