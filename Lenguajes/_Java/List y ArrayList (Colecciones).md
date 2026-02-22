
|**Concepto Clave**|**Nota Útil**|
|---|---|
|**List**|**Interfaz**. Define el contrato (qué se puede hacer). Mantiene el orden de inserción.|
|**ArrayList**|**Implementación**. Clase que usa un array redimensionable internamente.|
|**Acceso**|Muy rápido por índice ($O(1)$).|
|**Modificación**|Lento si se inserta/borra en medio ($O(n)$), rápido al final.|

#### 1. Concepto y Jerarquía

En Java, `List` es una sub-interfaz de `Collection`.

- **Ordenada:** Los elementos se guardan en el orden en que se insertan.
    
- **Duplicados:** Permite guardar elementos repetidos.
    
- **Índice:** Permite acceso posicional (como un array normal), empezando por 0.
    

**Diferencia Clave:**

- Un **Array** (`[]`) tiene tamaño fijo.
    
- Un **ArrayList** crece dinámicamente según sea necesario.
    

#### 2. Declaración (Buenas Prácticas)

Se recomienda programar contra la **interfaz**, no contra la implementación (Polimorfismo).

Java

```java
import java.util.List;
import java.util.ArrayList;

// MAL: Te ata a una implementación específica
ArrayList<String> lista1 = new ArrayList<>();

// BIEN: Más flexible. Puedes cambiar ArrayList por LinkedList luego sin romper el código.
List<String> lista2 = new ArrayList<>();
```

#### 3. Tipos de Datos (Wrappers)

Las colecciones en Java **NO** admiten tipos primitivos (`int`, `double`, `boolean`). Debes usar sus clases envoltorio (**Wrapper Classes**).

Java

```java
// ERROR: List<int> numeros = new ArrayList<>();
List<Integer> numeros = new ArrayList<>(); // CORRECTO
```

#### 4. Operaciones Principales

Java

```java
List<String> nombres = new ArrayList<>();

// 1. Inserción
nombres.add("Ana");
nombres.add("Juan");
nombres.add(1, "Pedro"); // Inserta en la posición 1, desplaza a Juan

// 2. Acceso
String nombre = nombres.get(0); // Devuelve "Ana"

// 3. Modificación
nombres.set(0, "Marta"); // Sustituye "Ana" por "Marta"

// 4. Eliminación
nombres.remove(1); // Elimina por índice
nombres.remove("Juan"); // Elimina por objeto (el primero que encuentre)

// 5. Información
int tamano = nombres.size(); // Tamaño actual
boolean existe = nombres.contains("Marta"); // true/false
```

#### 5. Funcionamiento Interno (Rendimiento)

`ArrayList` utiliza un **array normal** por debajo.

- Cuando el array se llena, Java crea uno nuevo (generalmente un 50% más grande), copia todos los elementos del viejo al nuevo y descarta el viejo.
    
- **Ventaja:** Leer datos (`get`) es instantáneo.
    
- **Desventaja:** Borrar o insertar al principio es costoso, porque Java tiene que "mover" todos los elementos siguientes una posición a la derecha o a la izquierda.
    

---

### Metadatos y Organización

**Lista de enlaces sugeridos:**

- [[Java - Arrays vs ArrayList]] (Comparativa directa)
    
- [[Java - Wrapper Classes]] (Integer, Double, etc.)
    
- [[Java - Bucle For-Each e Iteradores]] (Cómo recorrer listas)
    
- [[Java - LinkedList]] (La alternativa para muchas inserciones)
    

Tags recomendados:

#java #colecciones #estructuras_datos #arraylist #dam
