
| **Concepto clave** | **Nota útil**                                          |
| ------------------ | ------------------------------------------------------ |
| **Siglas**         | **P**roject **O**bject **M**odel.                      |
| **Formato**        | XML (Extensible Markup Language).                      |
| **Función**        | Es el "DNI" y el "plano de construcción" del proyecto. |
| **Ubicación**      | Siempre en la raíz del proyecto.                       |

#### 1. Coordenadas G.A.V. (La Identidad)

Para que Maven funcione, todo proyecto (o librería) debe ser único en el mundo. Se identifica mediante tres etiquetas obligatorias conocidas como **GAV**:

- **GroupId (`<groupId>`):** Identificador de la organización. Suele ser el dominio invertido.
    
    - _Ejemplo:_ `com.miempresa.ventas`
        
- **ArtifactId (`<artifactId>`):** Nombre del proyecto o módulo específico.
    
    - _Ejemplo:_ `api-facturacion`
        
- **Version (`<version>`):** Estado actual del desarrollo.
    
    - _Ejemplo:_ `1.0.0-SNAPSHOT` (Snapshot indica que está en desarrollo).
        

#### 2. Propiedades (`<properties>`)

Actúan como **variables globales**. Se usan para evitar repetir números de versiones y facilitar el mantenimiento (seguridad).

- Si usas la versión `5.3.20` de Spring en 10 dependencias distintas, defines una propiedad y la usas en todas. Cambiarla requiere tocar una sola línea.
    

**Ejemplo de Identidad y Propiedades:**

XML

```
<project>
    <groupId>es.miempresa</groupId>
    <artifactId>mi-app-gestion</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <java.version>17</java.version>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <jackson.version>2.15.0</jackson.version>
    </properties>
</project>
```

---
### Nota 2: Secciones Funcionales del POM

|**Concepto clave**|**Nota útil**|
|---|---|
|**Dependencies**|Lista de librerías externas que el proyecto necesita.|
|**Build**|Instrucciones de cómo compilar y empaquetar.|
|**Plugins**|Herramientas que ejecutan tareas (compilar, testear, crear `.jar`).|

#### 1. Dependencias (`<dependencies>`)

Aquí listamos las librerías externas. Maven leerá esto y descargará automáticamente los `.jar` necesarios (y sus transitivos) desde Maven Central.

- **Scope (Alcance):** Define cuándo se usa la librería.
    
    - `compile` (default): Siempre necesaria.
        
    - `test`: Solo para tests (ej. JUnit). No va al `.jar` final.
        
    - `runtime`: Solo al ejecutar (ej. Driver JDBC).
        

#### 2. Build y Plugins (`<build>`)

Define **cómo** se convierte el código en software ejecutable.

- Por defecto, Maven asume Java 1.5 (muy antiguo). **Es obligatorio** configurar el `maven-compiler-plugin` para decirle qué versión de Java usamos (ej. Java 17 o 21).
    
- Aquí también se configuran plugins de seguridad (OWASP) o de creación de ejecutables (Fat JARs).
    

**Ejemplo de Dependencias y Build:**

XML

```
<dependencies>
    <dependency>
        <groupId>com.fasterxml.jackson.core</groupId>
        <artifactId>jackson-databind</artifactId>
        <version>${jackson.version}</version>
    </dependency>

    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter</artifactId>
        <version>5.9.2</version>
        <scope>test</scope>
    </dependency>
</dependencies>

<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.11.0</version>
            <configuration>
                <source>${java.version}</source>
                <target>${java.version}</target>
            </configuration>
        </plugin>
    </plugins>
</build>
```

---

### Sugerencias de Enlazado y Tags

**Enlaces sugeridos:**

- [[Gestión de Dependencias: Manual vs Automática]] (Por qué usamos esto).
    
- [[Maven Ciclo de Vida]] (Qué hace Maven con este archivo: compile, package, install).
    
- [[Testing en Java]] (Uso del scope `test`).
    

Tags recomendados:

#maven #xml #devops #java #backend #configuracion