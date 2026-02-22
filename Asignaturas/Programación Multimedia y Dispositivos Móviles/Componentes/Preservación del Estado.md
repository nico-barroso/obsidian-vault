
Aunque el sistema intenta mantener todo vivo en memoria, hay diferencias en lo que se conserva:

### ✅ Lo que se conserva automáticamente

Gracias a que la [[Activity]] sigue "viva" en la pila:

- Texto introducido en un `EditText` (si tiene ID).
    
- Posición del scroll en listas.
    
- Variables de instancia (mientras el proceso no muera).
    

### ⚠️ El riesgo: Presión de memoria

Si el sistema operativo necesita RAM para otra tarea (como una llamada entrante o un juego pesado), puede **destruir** una Activity que esté en `onStop()`.

> [!DANGER] Importante para el desarrollo consciente Para evitar que el usuario pierda su progreso en estos casos extremos, debemos implementar **`onSaveInstanceState()`**. Esto guarda los datos críticos en un objeto `Bundle`que sobrevive incluso si el proceso es eliminado.