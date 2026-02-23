
|**Concepto clave**|**Nota útil**|
|---|---|
|**Patrón**|**Utility Class** (Clase de Utilidad) / Singleton implícito.|
|**Seguridad**|Uso de **Variables de Entorno** (`System.getenv`).|
|**Driver**|PostgreSQL (`jdbc:postgresql://...`).|
|**Objetivo**|Centralizar la conexión y evitar credenciales _hardcodeadas_.|

### Características del Diseño

#### 1. Seguridad y Entorno (12-Factor App)

El código no tiene la contraseña escrita directamente ("hardcoded"), salvo un valor por defecto. Utiliza `System.getenv()` para leer variables del sistema operativo.

- **Ventaja:** Permite subir el código a GitHub sin exponer contraseñas reales de producción.
    
- **Flexibilidad:** Puedes cambiar de base de datos local a producción cambiando variables de entorno (Docker, Kubernetes) sin recompilar el `.java`.
    

#### 2. Patrón Clase de Utilidad

- **`public final class`**: Impide que la clase sea heredada/extendida.
    
- **`private Db() {}`**: Constructor privado. **Impide instanciar** la clase (`new Db()`). Obliga a usar los métodos estáticos.
    

#### 3. Construcción de URL

Construye dinámicamente la URL JDBC concatenando host, puerto y nombre de BD.

- Formato: `jdbc:postgresql://[HOST]:[PORT]/[DB]`
    

### Código Java

Java

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.util.Properties;

public final class Db {  
  
    // Lectura de configuración desde VARIABLES DE ENTORNO
    // Estructura: getOrDefault("NOMBRE_VAR", "valor_por_defecto_local")
    private static final String HOST = System.getenv().getOrDefault("PG_HOST", "localhost");  
    private static final String PORT = System.getenv().getOrDefault("PG_PORT", "5432");  
    private static final String DB = System.getenv().getOrDefault("PG_DB", "LampreaDB");  
    private static final String USER = System.getenv().getOrDefault("PG_USER", "postgres");  
    private static final String PASS = System.getenv().getOrDefault("PG_PASS", "1940'");  
  
    // Construcción de la Connection String
    private static final String URL = "jdbc:postgresql://" + HOST + ":" + PORT + "/" + DB;  
  
    // Constructor privado: Evita instanciación (Utility Class)
    private Db() {}  
  
    /**
     * Obtiene una conexión activa a la base de datos.
     * @return Connection objeto JDBC
     * @throws SQLException Si fallan las credenciales o el servidor no responde
     */
    public static Connection getConnection() throws SQLException {  
        Properties p = new Properties();  
        p.setProperty("user", USER);  
        p.setProperty("password", PASS);  
        
        // Es recomendable añadir propiedades extra como timeout o SSL aquí
        // p.setProperty("ssl", "true");
        
        return DriverManager.getConnection(URL, p);  
    }  
} 
```
