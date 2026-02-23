
| **Concepto clave** | **Nota útil**                                                                          |
| ------------------ | -------------------------------------------------------------------------------------- |
| **Tipo**           | Patrón de Arquitectura de Software.                                                    |
| **Objetivo**       | **[[Separación de intereses]]**: desacoplar la interfaz (UI) de la lógica y los datos. |
| **Uso común**      | Desarrollo Web (Full Stack), Aplicaciones de Escritorio (Java Swing/JavaFX).           |
![Modelo Vista controlador](https://www.freecodecamp.org/espanol/news/content/images/2021/06/MVC3.png)
### Definición

El **MVC** es un estilo de arquitectura de software que separa los datos de una aplicación, la interfaz de usuario, y la lógica de control en tres componentes distintos.

### Componentes

![[Modelo]]

![[Vista]]

![[Controlador]]
### Flujo de Interacción

1. El **Usuario** interactúa con la interfaz (**Vista**).
    
2. El **Controlador** recibe la notificación de la acción.
    
3. El **Controlador** accede al **Modelo** para actualizarlo o recuperar datos.
    
4. El **Modelo** notifica el cambio de estado o devuelve datos.
    
5. El **Controlador** instruye a la **Vista** para que se actualice (o la Vista se actualiza observando al Modelo, dependiendo de la implementación).


---

### Sugerencias de Enlazado y Tags


- [[Separación de intereses]]
    
- [[Patrones de Diseño vs Patrones de Arquitectura]]
    
- [[Spring MVC]] (Si estudias Java/Spring)
    
- [[Arquitectura en Capas]]
    

Tags recomendados:

#arquitectura_software #patrones #dam #desarrollo_web #java