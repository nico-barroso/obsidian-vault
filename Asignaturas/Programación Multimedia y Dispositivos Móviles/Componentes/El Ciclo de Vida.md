### 🔼 El Relevo (Ir a SecondActivity)

Cuando `MainActivity` lanza a `SecondActivity`, ocurre un proceso coordinado en la [[Activity]]:

1. **MainActivity → `onPause()`**: Se detecta que va a dejar de ser la protagonista. Sigue parcialmente visible.
    
2. **MainActivity → `onStop()`**: Ya no es visible. Aquí es el momento ideal para liberar recursos pesados (conexiones, sensores).
    
3. **SecondActivity → `onCreate()` y `onResume()`**: La nueva actividad toma el control total.
    

Fragmento de código

```
graph TD
    A[MainActivity: Resumed] -->|Intent| B(MainActivity: onPause)
    B --> C(SecondActivity: onCreate/Start/Resume)
    C --> D(MainActivity: onStop)
    D --> E[MainActivity: Paused in Stack]
```

### 🔽 El Viaje de Vuelta (Cerrar SecondActivity)

Cuando el usuario pulsa "atrás" o se llama a `finish()`:

1. **SecondActivity** se despide ejecutando: `onPause()` → `onStop()` → **`onDestroy()`**.
    
2. Android **elimina físicamente** esa instancia de la pila y libera su memoria.
    
3. **MainActivity** vuelve al frente haciendo el camino inverso: `onRestart()` → `onStart()` → `onResume()`.