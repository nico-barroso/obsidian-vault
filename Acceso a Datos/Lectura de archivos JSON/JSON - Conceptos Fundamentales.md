
| **Concepto clave** | **Nota útil**                                                 |
| ------------------ | ------------------------------------------------------------- |
| **Definición**     | Formato de texto ligero para intercambio de datos1.           |
| **Origen**         | Formalizado en 2001 por Douglas Crockford2.                   |
| **Independencia**  | Inspirado en JS, pero compatible con Java, Python, C#, etc.3. |

### Definición y Propósito

JSON (**J**ava**S**cript **O**bject **N**otation) es un estándar diseñado para representar estructuras de datos complejas (objetos y listas) de forma legible para humanos y procesable por máquinas4. Su simplicidad lo ha convertido en el estándar _de facto_ para la comunicación Frontend-Backend y APIs REST

### Estructura Sintáctica

La sintaxis se basa en dos estructuras fundamentales6:

1. **Objeto:** Colección desordenada de pares clave-valor encerrada.
    
2. **Array:** Lista ordenada de valores encerrada en
    

**Tipos de Datos Soportados:**

| **Tipo**    | **Descripción**                           | **Ejemplo**     |     |
| ----------- | ----------------------------------------- | --------------- | --- |
| **String**  | Caracteres Unicode entre comillas dobles. | `"Hola"`        |     |
| **Number**  | Enteros o flotantes (sin distinción).     | `10`, `3.14`    |     |
| **Boolean** | Valor lógico.                             | `true`, `false` |     |
| **Null**    | Ausencia intencional de valor.            | `null`          |     |
| **Object**  | Estructura anidada.                       | `{"id": 1}`     |     |
| **Array**   | Colección de valores.                     | `[1, 2, 3]`     |     |

### JSON vs XML

Antes de JSON, el estándar era **XML** (Extensible Markup Language).

- **XML:** Verboso, requiere parsers complejos y etiquetas de cierre (`<tag>data</tag>`).
    
- **JSON:** Más ligero, menor tamaño de transmisión y mapeo directo a objetos en código
    

---

## ------ATOMIZACIÓN: Reglas de uso y estandarización

### Nota 2: JSON - Buenas Prácticas y Estándares

| **Concepto clave** | **Nota útil**                                              |     |
| ------------------ | ---------------------------------------------------------- | --- |
| **Encoding**       | Siempre usar **UTF-8** (RFC 8259)                          |     |
| **Comillas**       | Obligatorio usar comillas dobles `""` en claves y strings. |     |
| **Comentarios**    | **Prohibidos** en el estándar oficial                      |     |
|                    |                                                            |     |

### Reglas de Validación

Para garantizar que un JSON sea válido y procesable por cualquier sistema:

1. **Comillas Dobles:** A diferencia de JS, en JSON las comillas simples `''` provocan error de parsing. Las claves _siempre_ deben llevar comillas
    
2. **Sin Comentarios:** No se permiten `//` ni `/* */`. Si se necesita documentar, se debe añadir un campo de datos como `"_comentario"`.
    
3. **Unicidad de Claves:** No usar el mismo nombre de clave más de una vez en un objeto; el comportamiento es impredecible según el parser.
    

### Herramientas

- **Validación:** Usar herramientas como `jsonlint.com` para detectar errores de sintaxis (comas sobrantes, corchetes sin cerrar)
    
- **Formato:** Usar _pretty-printers_ para indentar y mejorar la legibilidad humana
    

---

## ------ATOMIZACIÓN: Implementación Técnica en Java

### Nota 3: Java - Persistencia JSON con Jackson

|**Concepto clave**|**Nota útil**|
|---|---|
|**Librería**|**Jackson** (`com.fasterxml.jackson`).|
|**Serializar**|Objeto Java $\rightarrow$ JSON (Texto).|
|**Deserializar**|JSON (Texto) $\rightarrow$ Objeto Java.|
|**Requisito POJO**|Es obligatorio tener un **Constructor Vacío** en el modelo.|

### Arquitectura de Implementación

Para implementar persistencia en JSON en un proyecto Java ([[Arquitectura en Capas]]), necesitamos tres componentes: Modelos (POJOs), Utilidad de E/S y un Controlador/Main.

#### 1. Modelos (POJOs)

Las clases deben tener **Getters/Setters** y un **Constructor Vacío**. Jackson usa reflexión; instancia la clase vacía y luego usa los setters para llenar los datos.

Java

```
package model;
public class Usuario {
    private int id;
    private String nombre;
    // ... otros atributos

    // OBLIGATORIO para Jackson: Constructor vacío
    public Usuario() {} 

    // Constructor con parámetros para uso normal
    public Usuario(int id, String nombre) { 
        this.id = id; 
        this.nombre = nombre; 
    }
    // Getters y Setters...
}
```

#### 2. Utilidad Genérica (`JsonIO`)

Usamos genéricos `<T>` para no duplicar código. Esta clase envuelve al `ObjectMapper` de Jackson.

- `enable(SerializationFeature.INDENT_OUTPUT)`: Activa el _pretty-print_ para que el JSON se guarde con saltos de línea y tabulaciones, en vez de una sola línea comprimida.
    

Java

```
package util;
import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.SerializationFeature;
import java.io.File;
import java.io.IOException;

public class JsonIO {
    // Instancia estática del mapper (Heavy object, mejor reutilizar)
    private static final ObjectMapper MAPPER = new ObjectMapper()
            .enable(SerializationFeature.INDENT_OUTPUT);

    private JsonIO() {} // Evitar instanciación

    // Serialización (Java -> JSON)
    public static <T> void write(File file, T data) throws IOException {
        file.getParentFile().mkdirs(); // Asegura que la carpeta exista
        MAPPER.writeValue(file, data);
    }

    // Deserialización (JSON -> Java)
    public static <T> T read(File file, Class<T> type) throws IOException {
        return MAPPER.readValue(file, type);
    }
}
```

#### 3. Ejecución (`MainApp`)

Gestión del flujo de datos usando `java.nio.file.Path` para rutas relativas seguras.

Java

```
// Definición de ruta segura (independiente del SO)
private static final Path RUTA = Paths.get("data", "biblioteca.json");

// Lógica de carga
File json = RUTA.toFile();
if (!json.exists()) {
    // Caso 1: No hay datos, creamos, serializamos y guardamos
    Biblioteca biblio = cargaDatosDummy();
    JsonIO.write(json, biblio);
}
// Caso 2: Leemos (Deserializamos) pasando la clase contenedora
Biblioteca datos = JsonIO.read(json, Biblioteca.class);
```

---

### Sugerencias de Enlazado y Tags

**Enlaces sugeridos:**

- [[Java NIO vs IO]] (Uso de `Path` vs `File`).
    
- [[Genéricos en Java]] (Explicación de `<T>`).
    
- [[API REST con Spring Boot]] (Donde más se usa JSON).
    
- [[Serialización de Objetos]]
    

Tags recomendados:

#json #jackson #java #persistencia #dam #backend #formatos_datos