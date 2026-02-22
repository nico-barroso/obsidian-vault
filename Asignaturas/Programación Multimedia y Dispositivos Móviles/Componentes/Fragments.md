Un fragmento, es en esencia una pieza modular de la interfaz de usuario que vive dentro de una Activity.

Estos fragmentos son **componentes atómicos** que permiten hacer interfaces complejas y adaptables sin tener que crear una Activity nueva para cada pantalla

Existen para suplir tres necesidades:

- **Reutilización:** Puedes usar el mismo fragmento de "Perfil" en cinco pantallas distintas.
  
- **Adaptabilidad:** Permiten crear diseños responsivos (Multi-pane layouts).
  
- **Modularidad:** Separas la lógica de la UI del contenedor principal (la Activity).

## [[El Ciclo de Vida]]

Un fragmento tiene **dos ciclos de vida**: el suyo propio y el de su **vista**.

> [!CAUTION] Error común El Fragment puede seguir existiendo en la memoria aunque su interfaz (XML) haya sido destruida para ahorrar RAM.

| **Fase**     | **Método**        | **Qué hacer aquí**                                                              |
| ------------ | ----------------- | ------------------------------------------------------------------------------- |
| **Vínculo**  | `onAttach()`      | El fragmento sabe en qué Activity está.                                         |
| **Creación** | `onCreate()`      | Inicializas variables que **no** dependen de la interfaz.                       |
| **Interfaz** | `onCreateView()`  | Inflas el layout XML. Solo devuelves la vista.                                  |
| **Listos**   | `onViewCreated()` | **El más importante.** Aquí haces los `findViewById` o vinculas el ViewBinding. |
| **Limpieza** | `onDestroyView()` | La vista desaparece. Limpias referencias a la UI para evitar fugas de memoria.  |
## 3. Comunicación: ¿Cómo hablan entre ellos?

Siguiendo principios de **Clean Code** y desacoplamiento, un fragmento nunca debería hablar directamente con otro fragmento.

1. **Fragment → Activity:** A través de una `Interface` o un `ViewModel` compartido.
    
2. **Activity → Fragment:** Usando `bundle` de argumentos al crearlo.
    
3. **Fragment ↔ Fragment:** La forma moderna y recomendada es el **Shared ViewModel**. Ambos observan los mismos datos.
    

---

## 4. El "FragmentManager" y la Pila

Así como la Activity se apila en el sistema, los fragmentos se apilan dentro de la Activity mediante transacciones.

Kotlin

```
supportFragmentManager.commit {
    replace(R.id.container, MiNuevoFragment())
    addToBackStack(null) // Esto permite que el botón "Atrás" funcione para el fragmento
}
```

---

## 5. Puntos Clave para tu Bitácora

- **Constructor Vacío:** **NUNCA** crees un constructor con parámetros en un Fragment. Android necesita el constructor vacío para recrear el fragmento si el sistema lo mata. Usa `Arguments` (Bundles).
    
- **Single Activity Architecture:** La tendencia actual es tener **una sola Activity** y que todo el resto de la App sean Fragments moviéndose por el `Navigation Component`.
    
- **View Lifecycle:** Recuerda siempre usar `viewLifecycleOwner` en lugar de `this` cuando uses LiveData o Flows dentro de un fragmento. Así evitas que los observadores sigan vivos cuando la vista ya no existe.