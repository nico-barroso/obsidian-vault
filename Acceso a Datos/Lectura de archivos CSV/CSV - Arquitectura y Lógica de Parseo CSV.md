
|**Concepto Clave**|**Nota Útil**|
|---|---|
|**Objetivo**|Leer CSV respetando cabeceras y registros complejos (comillas).|
|**Patrón**|Separación de Responsabilidades (UI vs Lógica vs Datos).|
|**Algoritmo**|Parseo carácter a carácter con **Máquina de Estados**.|

#### 1. Arquitectura del Proyecto

El proyecto se organiza mediante **aislamiento por paquetes** para desacoplar la lógica de negocio de la ejecución. Esto permite cambiar la forma de leer archivos sin romper la lógica de procesamiento de datos.

- **Estructura de Directorios:**
    
    - `root/data/`: Almacén de archivos `.csv` (fuera del código fuente).
        
    - `src/app/`: Punto de entrada (`main`). Capa de ejecución.
        
    - `src/csv/`: Lógica pura. No sabe de archivos, solo de Strings y Datos.
        
- **Roles de las Clases:**
    
    1. `AppLeerCSV` (Paquete `app`): **Orquestador**. Verifica rutas, abre flujos y coordina.
        
    2. `CsvUtils` (Paquete `csv`): **Helper**. Procesamiento estático de texto.
        
    3. `CsvTable` (Paquete `csv`): **Modelo**. Estructura en memoria (Mapa/Lista).
        
    4. `CsvPrinter` (Paquete `csv`): **Vista**. Pinta los resultados en consola.
        

#### 2. Clase de Utilidad: `CsvUtils`

Esta clase sigue el patrón **Helper Class**:

- **Constructor Privado:** `private CsvUtils() {}`. Bloquea la creación de instancias (`new CsvUtils()`) porque no tiene estado interno que guardar. Es una caja de herramientas.
    
- **Método Estático:** `static parseCSVLine`. Se llama directamente desde la clase.
    

#### 3. Lógica del Algoritmo (State Machine)

El desafío es distinguir una coma separadora de una coma dentro de un texto (ej: `"Madrid, España"`). Usamos una variable de control de flujo (`boolean enComillas`).

![Imagen de finite state machine diagram](https://encrypted-tbn3.gstatic.com/licensed-image?q=tbn:ANd9GcS3Kl-XIXObCnfnpzUjf1MOhc8Wo4QzkbSlejUuvgZrBkuyy7g4SX17KhXj2NfQ0jZr_8q-Fa0JL5VC-7WolX_bz2w6wMzC552EwjArPc_0KJnP8N8)

Getty Images

**Paso a paso del algoritmo:**

1. **Iteración:** Recorremos la línea carácter a carácter.
    
2. **Detección de Comillas (`"`):**
    
    - Si encontramos `""` (dos seguidas): Es una comilla escapada (literal).
        
    - Si es una sola: Invertimos el interruptor `enComillas` (True <-> False).
        
3. **Detección de Comas (`,`):**
    
    - Si `enComillas == true`: La coma es texto. Se añade al buffer.
        
    - Si `enComillas == false`: Es separador. Guardamos el dato y limpiamos buffer.
        
4. **Acumulación:** Usamos `StringBuilder` para ir "pegando" los caracteres válidos eficientemente.
    

Java

```
package csv;
import java.util.ArrayList;
import java.util.List;

public class CsvUtils {

    private CsvUtils() {} // Constructor privado

    public static List<String> parseCSVLine(String line) {
        List<String> out = new ArrayList<>();
        StringBuilder sb = new StringBuilder(); 
        boolean enComillas = false; // ESTADO

        for (int i = 0; i < line.length(); i++) {
            char ch = line.charAt(i);

            if (ch == '"') {
                // Lógica de comillas escapadas vs cambio de estado
                if (enComillas && i + 1 < line.length() && line.charAt(i + 1) == '"') {
                    sb.append('"');
                    i++; 
                } else {
                    enComillas = !enComillas; // Cambio de estado
                }
            } 
            // La coma solo separa si NO estamos en modo "enComillas"
            else if (ch == ',' && !enComillas) {
                out.add(sb.toString());
                sb.setLength(0); 
            } 
            else {
                sb.append(ch);
            }
        }
        out.add(sb.toString()); // Añadir último campo
        return out;
    }
}
```

---

### Nota 2: Implementación de Lectura (App)

|**Concepto clave**|**Nota útil**|
|---|---|
|**Recurso**|`BufferedReader` (Lectura eficiente línea a línea).|
|**Seguridad**|`Try-with-resources` garantiza el cierre del fichero.|
|**Codificación**|`StandardCharsets.UTF_8` es obligatorio para evitar errores de símbolos.|

#### 1. Gestión de Recursos (Try-with-resources)

Antiguamente, si el programa fallaba antes del .close(), el archivo quedaba bloqueado en memoria (Memory Leak).

Java introdujo la sintaxis try (...). Cualquier objeto dentro del paréntesis que implemente AutoCloseable se cerrará automáticamente al llegar a la llave de cierre }, ocurra un error o no.

#### 2. Gestión de Rutas (NIO)

- **Problema:** Usar Strings (`"C:\Datos\..."`) falla si cambias de Windows a Linux/Mac.
    
- **Solución `Paths.get`:** Construye la ruta usando el separador correcto del sistema operativo actual.
    
- **Validación:** Antes de leer, intentamos crear el directorio con `Files.createDirectories`. Si ya existe, no hace nada; si no, lo crea.
    

#### 3. Bucle de Lectura

El patrón estándar de lectura en Java es:

while ((linea = br.readLine()) != null)

- **Paso 1:** Lee una línea del buffer.
    
- **Paso 2:** Asigna el valor a la variable `linea`.
    
- **Paso 3:** Comprueba si es `null` (fin del archivo).
    
- **Paso 4:** Si no es null, entra al bucle y procesa.
    

Java

```
package app;

import csv.CsvUtils;
import java.io.BufferedReader;
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.*;
import java.util.List;

public class AppLeerCsv {

    // Ruta relativa a la carpeta raíz del proyecto
    private static final Path RUTA = Paths.get("data", "clientesResumen.csv");

    public static void main(String[] args) {
        
        // 1. Asegurar entorno (Directorio)
        try {
            Files.createDirectories(RUTA.getParent());
        } catch (IOException e) {
            System.err.println("Error creando directorios: " + e.getMessage());
            return; 
        }

        // 2. Apertura Segura (Try-with-resources)
        try (BufferedReader br = Files.newBufferedReader(RUTA, StandardCharsets.UTF_8)) {

            // Lectura de cabecera (primera línea)
            String linea = br.readLine();
            if (linea == null) {
                System.err.println("CSV Vacío");
                return;
            }

            List<String> headers = CsvUtils.parseCSVLine(linea); // Uso de la Utilidad (Nota 1)
            System.out.println("Cabeceras: " + headers);

            // 3. Bucle de datos
            while ((linea = br.readLine()) != null) {
                List<String> campos = CsvUtils.parseCSVLine(linea);
                // Procesamiento de datos...
            }

        } catch (NoSuchFileException e) {
            System.err.println("Fichero no encontrado: " + RUTA.toAbsolutePath());
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

|
---

### Metadatos Globales

**Enlaces sugeridos:**

- [[Máquina de Estados Finitos]] (Lógica del parser)
    
- [[Java Exception Handling]] (Try-catch)
    
- [[Java I/O vs NIO]] (Files y Paths)
    
- [[Patrones de Diseño Java]] (Clase de Utilidad)
    

Tags:

#java #algoritmos #csv #io #dam #backend

# Clase 3
En este proyecto haremos 2 listas
Una primera lista que contará con cada uno de los campos de la cabecera

Una segunda lista que en cada posición de la lista contará con un mapa clave valor, en la que la clave será el nombre de la cabecera y el valor el valro del campo. Cada posiciónd e la lista sderá una fila del archivo
Para imp`lementar un map hay:
HashMap -> el problema no hay orden, es aleatorio
treemap-> se oordenan segun la clave (alfabeticamente)
linkedhashmap -> ordena segun insercion (por el orden que insertes
creamos una clase CsvTable) Si una lista no la pones final, podrian recolocar la dirección de memoria, reorganizandolo y podría implicar joder la memoria