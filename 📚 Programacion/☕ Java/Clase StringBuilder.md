---
tags: [java, strings, optimizacion]
category: Programacion
related: [[List y ArrayList (Colecciones)]]
---

# StringBuilder

| **Concepto Clave** | **Nota Útil** |
|---|---|
| **StringBuilder** | Clase mutable para manipular strings de forma eficiente. |
| **Problema de String** | Los objetos `String` son inmutables; concatenar en bucles consume mucha memoria. |

## Problema: Inmutabilidad de String

Cada vez que modificas un String, Java crea un **nuevo objeto** en memoria. En bucles puede saturar la memoria.

## Solución: StringBuilder

```java
StringBuilder sb = new StringBuilder();
sb.append("Hola ");
sb.append("Mundo");
String resultado = sb.toString();
```

> Ver: [[List y ArrayList (Colecciones)|Colecciones]]