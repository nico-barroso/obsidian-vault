---
tags: [android, activity, componentes]
category: Mobile
related: [[Fragments]], [[Back Stack (Pila de Actividades)]], [[Preservación del Estado]], [[El Ciclo de Vida]]
---

# Activity

Componente que representa una **pantalla** de la app.

## Navegación

- **Intent**: Mensajero para crear nueva Activity
- `startActivity(intent)`

## Concepts

| Concepto | Descripción |
|---|---|
| [[Back Stack (Pila de Actividades)\|Back Stack]] | Pila LIFO |
| Lifecycle | `onCreate`, `onStart`, `onResume`... |
| Preservación | `onSaveInstanceState` |
| [[Fragments]] | Mini-activities dentro de Activity |

## Ejemplo

```kotlin
val intent = Intent(this, SecondActivity::class.java)
startActivity(intent)
```

> Ver: [[Fragments]], [[El Ciclo de Vida]], [[Preservación del Estado]]