## La Pila de Actividades (Back Stack)

Android gestiona las [[Activity]] mediante una estructura de datos tipo **LIFO** (Last In, First Out).

> [!ABSTRACT] Analogía de los platos Imagina una pila de platos. Cada vez que abres una Activity, pones un plato nuevo encima del anterior.
> 
> - El usuario **solo interactúa** con el plato superior.
>     
> - Los platos de abajo **no desaparecen**: siguen ahí, pausados y ocupando memoria, manteniendo su estado intacto.
>