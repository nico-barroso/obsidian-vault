Una **Activity** es el componente que combina la interfaz visual (XML/Compose) con la lógica de interacción. Es, en esencia, cada "pantalla" de la aplicación.

Para navegar entre ellas, utilizamos un **Intent**, que actúa como el mensajero que solicita al sistema crear una nueva instancia de una Activity y colocarla sobre la anterior.

| **Concepto Clave**                   | **Regla Técnica**                                                                 | **Acción / Best Practice (Kotlin)**                                                                                   |
| ------------------------------------ | --------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| [[Back Stack (Pila de Actividades)]] | Estructura **LIFO**. Cada nueva Activity se apila; la anterior queda en `onStop`. | **Controlar la profundidad:** No acumules platos innecesarios; consume RAM y confunde al usuario.                     |
| **Lifecycle**                        | El sistema llama a los métodos automáticamente en un orden estricto.              | **Override consciente:** Sobrescribe `onPause`/`onStop` para liberar recursos (sensores, timers) y evitar fugas.      |
| **Preservación**                     | El estado de la UI sobrevive a la pausa, pero NO a la muerte por RAM.             | **`onSaveInstanceState`:** Úsalo para datos críticos. Para datos de UI complejos, usa **ViewModel**.                  |
| **`finish()`**                       | Mata la instancia actual y la elimina físicamente de la pila.                     | **Uso estratégico:** Llama a `finish()` en pantallas de Login o Splash para que no vuelvan a aparecer al dar "atrás". |
| **[[Fragments]]**                    | Son "mini-activities" que viven dentro de una Activity host.                      | **Single Activity Architecture:** Usa una sola Activity y navega intercambiando Fragments para mayor fluidez.         |
| **Back Stack Fragment**              | La Activity gestiona su propia pila interna de Fragments.                         | **`addToBackStack()`:** Decidir explícitamente si el botón "Atrás" debe cerrar el Fragment o solo la Activity.        |

#activity