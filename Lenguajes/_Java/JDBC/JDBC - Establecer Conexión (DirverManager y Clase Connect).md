
|**Concepto clave**|**Nota útil**|
|---|---|
|**Clase**|`java.sql.DriverManager`.|
|**Objeto**|`Connection` (Interfaz que representa la sesión con la BD).|
|**Método**|`getConnection(url, props)` es el patrón de fábrica.|
|**Excepción**|**Siempre** lanza `SQLException` (obligatorio gestionarla).|

### Descripción

Para conectar Java con una base de datos relacional, utilizamos la API **JDBC**. La clase `DriverManager` actúa como puente: busca el driver adecuado para la base de datos (MySQL, PostgreSQL, Oracle) y devuelve un objeto `Connection` activo.

El objeto Properties:

En lugar de pasar usuario y contraseña como argumentos sueltos, tu código los encapsula en un objeto Properties. Esto es una buena práctica porque:

1. Permite añadir más configuraciones (timeout, ssl, encoding) sin cambiar la firma del método.
    
2. Mantiene el código más limpio.
    

### Implementación

Este método suele encapsularse en una clase dedicada (ej. `DbConnection` o `DatabaseManager`) para no repetir el código de conexión en cada consulta.

Java

```java
import java.sql.Connection;  
import java.sql.DriverManager;  
import java.sql.SQLException;  
import java.util.Properties;  
  
/**  
 * Clase de utilidad para la gestión de la conexión con PostgreSQL. * Sigue el patrón de diseño Singleton (instancia única) para la configuración. */public final class Db {  
  
    // --- Configuración mediante Variables de Entorno ---  
    // Se prioriza la configuración del sistema para entornos de producción/Docker.    private static final String HOST = System.getenv().getOrDefault("PG_HOST", "localhost");  
    private static final String PORT = System.getenv().getOrDefault("PG_PORT", "5432");  
    private static final String DB   = System.getenv().getOrDefault("PG_DB",   "LampreaDB");  
    private static final String USER = System.getenv().getOrDefault("PG_USER", "postgres");  
    private static final String PASS = System.getenv().getOrDefault("PG_PASS", "1940'");  
  
    // JDBC URL: Protocolo + Subprotocolo (Postgres) + Host:Port / Database  
    private static final String URL  = "jdbc:postgresql://" + HOST + ":" + PORT + "/" + DB;  
  
    /**  
     * Constructor privado para evitar la instanciación de la clase.     * Al ser una clase de utilidad, solo accedemos a sus métodos estáticos.     */    private Db() {}  
  
    /**  
     * Establece y retorna una conexión activa con la base de datos.     * * @return Connection objeto de conexión JDBC.     * @throws SQLException Si ocurre un error al conectar o las credenciales son inválidas.  
     */    public static Connection getConnection() throws SQLException {  
        // Configuramos las propiedades de autenticación  
        Properties p = new Properties();  
        p.setProperty("user", USER);  
        p.setProperty("password", PASS);  
  
        // El DriverManager gestiona el conjunto de drivers JDBC disponibles  
        return DriverManager.getConnection(URL, p);  
    }  
}
```

### Anatomía de la URL JDBC

La cadena de conexión es crítica. Si falla, el 90% de las veces es por esto.

Formato: ```jdbc:[subprotocolo]://[host]:[puerto]/[base_de_datos]```

- `jdbc`: Protocolo principal.
    
- `mysql`: (o `postgresql`, `oracle`) Indica qué driver usar.
    
- `localhost`: Dirección IP del servidor.
    
- `3306`: Puerto por defecto de MySQL.
    
- `/tienda`: Nombre de la base de datos a la que entras.


### Nota Importante: Gestión de Recursos

El objeto `Connection` devuelto **debe cerrarse** siempre. Como implementa `AutoCloseable`, lo ideal es usarlo donde se llame dentro de un **Try-with-resources**:

Java

```java
// Ejemplo de uso
try (Connection con = DbConnection.getConnection()) {
    System.out.println("Conectado con éxito.");
    // Lógica de consultas...
} catch (SQLException e) {
    e.printStackTrace();
}
```

---

### Sugerencias de Enlazado y Tags

**Enlaces sugeridos:**

- [[Java Try-with-resources]] (Esencial para cerrar la conexión).
    
- [[Patrón Singleton]] (A menudo se usa para no crear múltiples instancias del gestor).
    
- [[Drivers JDBC]] (Tipos de drivers y dependencias Maven).
    

Tags recomendados:

#java #jdbc #sql #database #backend #dam