```kotlin
//Ejemplo de implementación
package com.example.bettertimetoseeyou.model  
  
data class HourWeather (  
    val hour: String,  
    val tempC: Int,  
    val iconRes: Int  
)
```

Una [Data Class] es una clase especializada cuya función principal es **almacenar datos**. El compilador de Kotlin genera automáticamente varios métodos estandard.

#### Requisitos
1. El constructor primario debe tener al menos un parámetro.
2. Todos los parámetros del constructor primario deben marcarse como val o var.
3. No pueden ser abstractas, open, sealed o inner

#### Métodos
Al definir la [[Data Class]], Kotlin te regala  unas implementaciones:

1. `equals()` y `hashCode()`**: Compara objetos por su **contenido** y no por su referencia de memoria. Dos objetos con los mismos datos serán considerados iguales.

2. **`toString()`**: Devuelve una cadena legible con el nombre de la clase y sus propiedades (ej: `User(name=Nico, age=25)`), ideal para tu _Code Journal_.

3. **`copy()`**: Permite crear una copia de un objeto cambiando solo algunas de sus propiedades, manteniendo la inmutabilidad.

4. **`componentN()`**: Habilita el **destructuring declarations**, permitiendo desglosar un objeto en variables individuales de un solo golpe.