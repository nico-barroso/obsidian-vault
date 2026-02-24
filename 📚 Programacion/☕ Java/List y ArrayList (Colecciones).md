---
tags: [java, colecciones, estructuras-datos]
category: Programacion
related: [[Clase StringBuilder]]
---

# List y ArrayList

| **Concepto Clave** | **Nota Útil** |
|---|---|
| **List** | Interfaz. Mantiene el orden de inserción. |
| **ArrayList** | Implementación con array redimensionable. |
| **Acceso** | O(1) por índice. |
| **Modificación** | O(n) si es en medio, O(1) al final. |

#### 1. Concepto y Jerarquía

En Java, `List` es una sub-interfaz de `Collection`.

- **Ordenada:** Los elementos se guardan en el orden en que se insertan.
    
- **Duplicados:** Permite guardar elementos repetidos.
    
- **Índice:** Permite acceso posicional (como un array normal), empezando por 0.
    

**Diferencia Clave:**

- Un **Array** (`[]`) tiene tamaño fijo.
    
- Un **ArrayList** crece dinámicamente según sea necesario.
    

## Declarar (Programar contra interfaz)

```java
// MALO: Te ata a una implementación
ArrayList<String> lista1 = new ArrayList<>();

// BUENO: Flexible
List<String> lista2 = new ArrayList<>();
```

## Wrappers (No primitivos)

```java
// ERROR: List<int> numeros = new ArrayList<>();
List<Integer> numeros = new ArrayList<>(); // CORRECTO
```

## Operaciones

```java
List<String> nombres = new ArrayList<>();

nombres.add("Ana");           // Añadir
nombres.add(1, "Pedro");     // Insertar en posición
String nombre = nombres.get(0);  // Acceso
nombres.set(0, "Marta");      // Modificar
nombres.remove(1);            // Eliminar por índice
nombres.remove("Juan");      // Eliminar por objeto
nombres.size();               // Tamaño
nombres.contains("Marta");    // Buscar
```

> Ver: [[Clase StringBuilder]] para strings eficientes
