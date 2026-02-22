
|**Concepto Clave**|**Nota Útil**|
|---|---|
|**StringBuilder**|Clase mutable para manipular cadenas de caracteres de forma eficiente.|
|**Problema de String**|Los objetos `String` son inmutables; concatenar en bucles consume mucha memoria.|
|**Uso principal**|Construcción dinámica de strings (bucles, formateo complejo).|

#### Problema: Inmutabilidad de la clase String

En Java, la clase `String` es inmutable.

- **Gestión de memoria:** Cada vez que modificas un String (por ejemplo, en una concatenación dentro de un bucle `for`), Java no modifica el objeto original.
    
- **Consecuencia:** Se crea un **nuevo objeto** en memoria para cada modificación, descartando el anterior.
    
- **Riesgo:** Esto puede saturar la memoria (el "buffer" o Heap) y provocar problemas de rendimiento o un desbordamiento si la operación es masiva ("hacer que pete").


#### Solución: StringBuilder

La clase `StringBuilder` permite modificar la cadena de caracteres sin crear nuevos objetos constantemente.

- Trabaja sobre un mismo objeto (mutable).
    
- Gestiona un buffer interno redimensionable.
    
- Es la forma segura y eficiente de componer acciones completas o cadenas largas.


#### Ejemplo de Declaración

Se instancia como un objeto nuevo para empezar a manipular la cadena:

Java

```
// Inicialización de un StringBuilder vacío
StringBuilder sb = new StringBuilder();

// Ejemplo de uso típico (append)
sb.append("Hola ");
sb.append("Mundo");
String resultado = sb.toString(); // Convierte a String final
```

---

### Metadatos y Organización

**Lista de enlaces sugeridos (Copiar y pegar en Obsidian):**

- [[Java - Clase String]]
    
- [[Java - Gestión de Memoria y Garbage Collector]]
    
- [[Java - Bucles y Estructuras de Control]]
    

Tags recomendados:

#java #programacion #optimizacion #estructuras_datos #dam

---

**¿Quieres que genere una nota adicional comparando `StringBuffer` vs `StringBuilder` (por temas de hilos/concurrencia) o prefieres seguir con otro tema?**