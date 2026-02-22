Es una **función estándar** que crea un StringBuilder internamente y devuelve un String.
Es la versión más eficiente y legible que [[Kotlin]] ofrece para concatenar y trabajar con Strings (*evitando el uso excesivo del "+"*)
```kotlin
 val texto = buildString {

    append("Hola")

    append(" ")

    append("mundo")

}
```


> [!NOTE] Nico Nota
> Se puede incluso meter directamente en if's y otras funciones sin necesidad de asignarla a una variable 
>
> 
> 
> 

```
val salida = if (num != null) {  
  
    buildString {  
        appendLine("Entrada = ")  
        appendLine("Tipo número = ${tipoNumero(num)}")  
        appendLine("Suma hasta = ${sumaHasta(num)}")  
        appendLine("Es par = ${esPar(num)}")  
    }  
} else {  
    buildString {  
        appendLine("Entrada = $valor")  
        appendLine("Longitud = ${valor.length}")  
    }
    ```
   ```
    
