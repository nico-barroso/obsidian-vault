Novedades
Nueva organización de carpets
Linear Layout
[[ListView]] y [[RecyclerView]]
Creación de [[Modelo de Datos]]

> [!Temas tratados]
> Nueva organización de carpets
Linear Layout
[[ListView]] y [[RecyclerView]]
Creación de [[Modelo de Datos]]
> [[viewBinding]]

## Configuraciones

Añadimos en el gradle.kts en el buildTypes para añadir el [[viewBinding]] e importamos el RecyclerView 
```kotlin
// ------ build.gradle.kts (:app)------------
buildTypes{...}
-> buildFeatures{
		viewBinding = true
}
{...}
dependencies{
	implementation(libs.androidx.recyclerview)
}
```

2. Creamos el Android Resource Directory (layaout) en el res
3. Creamos un package, un package es una carpeta con referencias para poder referenciar contenidos del resto del paquete sin importar nada


## Personalización de Strings
En la carpeta res, tenemos values y dentro strings xml, es ahí donde tocamos los strings


# Archivo MainActivity

Probamos un par de funciones y sintáxis básica de Kotlin para aprender como se trabaja con Kotlin

> [!NOTE]
>   En el MainActivity, como es el único que exister y no necesitamos llamarlo desde fuera, mejor.  
 La filosofía es restringir al máximo, si funciona con private, lo dejamos private.


```kotlin
//MaiActivity.kt
package com.example.bettertimetoseeyou  
  
import androidx.appcompat.app.AppCompatActivity  

class MainActivity : AppCompatActivity() {  
//Single Expresión function en Kotlin
    private fun esPar(n: Int) = n % 2 == 0  
//Vector de números para probar forEach 
    private fun recorreNumeros() {   
        val numeros = arrayOf(3, 5, 6, 7)  
        numeros.forEach { num ->  
            if (esPar(num)) {  
                println("Numero: $num es par")  
            } else {  
                println("Numero: $num es impar")  
            }  
        }  
    }  
  
    private fun sumaHasta(n: Int): Int {  
        var total = 0  
        for (i in 1..n) {  
            total += i  
        }  
        return total  
    }  
  
    //Creciendo 2  
    private fun sumaHasta2(n: Int): Int {  
        var total = 0  
        for (i in 1 until n step 2) {  
            total += i  
        }  
        return total  
    }  
  
    //Decreciendo  
    private fun sumaHasta3(n: Int): Int {  
        var total = 0  
        for (i in 1 downTo n step 2) {  
            total += i  
        }  
        return total  
    }  
  
    private fun tipoNumero(n: Int): String {  
        //Necesita un elemento default para que funcione  
        return when {  
            n < 0 -> "Negativo"  
            n == 0 -> "Cero"  
            else -> "Positivo"  
        }  
    }  
}
```


### 23/10/2025
Primero vamos a crear una función para que acepte un [[CallBack]]

Empezamos en nuestro onCreate invocar los contentView
```kotlin 
override fun onCreate(savedInstanceState: Bundle?){  
    //Tenemos que lñlamar al metodo original y sobreescribirlo  
    super.onCreate(savedInstanceState)  
    setContentView(R.layout.activity_main)  
  
    val tvTitulo = findViewById<TextView>(R.id.tvTitulo)  
    val etEntrada = findViewById<EditText>(R.id.etEntrada)  
    val btnProcesar = findViewById<Button>(R.id.btnProcesar)  
    val tvResultado = findViewById<TextView>(R.id.tvResultado)
    ```
    Luego cambiamos el texto del título
```kotlin

tvTitulo.text = "KOTLIN DEMO"

```

Queremos  hacer que el botón pueda ver texto ____cambiar

Cambiamos la actividad principal en el AndroidManifest añadiendo otro activity
## Ciclos de Activity 30/10/25
Tenemos que crear una segunda activity, para ello es importante tener en cuenta las siguientes cosas:
1. Creación de un nuevo layaout para la siguiente activity

> [!IMPORTANT]
> 1. Añadir la siguiente activity al Android Manifest, SE TENDRÁ QUE PONER EL NOMBRE DE LA CLASE ``` 
>    <activity android:name=".SecondActivity" android:exported="false" />```

Para movernos entre activities tenemos que crear un [[Intent]], el Intent tendrá entre sus parametros la segunda actividad, heredará de class y lueog con putExtra pdoremos enviar datos de uno en uno
```kotlin
val intent = Intent(this, SecondActivity::class.java).apply{  
//          En el caso de querer enviar d waatos a la otra actividad  
                putExtra(TEXTO1, textoEntrada)  
                if (numero!= null) putExtra(TEXTO2, numero)  
            }  
            startActivity(intent)  
        }
        ```
        