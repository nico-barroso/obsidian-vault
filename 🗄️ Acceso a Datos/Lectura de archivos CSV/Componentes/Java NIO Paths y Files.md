
| **Concepto clave**    | **Nota útil**                                                                            |
| --------------------- | ---------------------------------------------------------------------------------------- |
| **Paths.get()**       | Crea rutas independientes del SO (usa `/` o `\` según corresponda).                      |
| **Ruta Relativa**     | `Paths.get("data", "archivo.csv")` busca en la raíz del proyecto, no en C:/.             |
| **CreateDirectories** | `Files.createDirectories` no lanza error si ya existe; crea toda la jerarquía necesaria. |

Gestión de Rutas:

Es vital no "hardcodear" rutas absolutas (ej: C:/Users/...) para que el proyecto funcione en cualquier ordenador.

**Validación de existencia:**

1. **Directorio:** Se intenta crear antes de operar. Si falla, suele ser por permisos.
    
2. **Fichero:** Al intentar abrir el flujo de lectura (`newBufferedReader`), si no existe, lanza `NoSuchFileException`. Es mejor capturar esta excepción específica que una genérica.

```java
`private static final Path RUTA = Paths.get("<DIRECTORIO>", "<ARCHIVO>");`
```
