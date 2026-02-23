---
aliases:
  - ¿Qué pasa realmente al abrir otra activity?
---
Activity son las pantallas con vistas y la lógica que hay detrás.
A nivel de código, llamaremos a una función llamada Intent, que creará una nueva instancia de Second Activity y kla coloca encima de [[_Kotlin|MainActivity]] haciendo una **pila de Activities (Activity Stack)** La MainActivity no desaparece, queda pausada

La pila de activities: visualizada como platos
Lo que ocurre es que la main deja de estar visible pero sigue viva en memoria, todo los datos, registros o lo que el usuario haya subido o marcadado se guarda en emmoria ocupando el mismo espacio. El usuario solo puede interactuar con el primer plato, aunque los platos sigan estando ahi uno encima de otro.

## El ciclo de vida

MainAcitivity -> onPause()
La actifvidad actual detecta que pasa a memoria y que va a estar parcialmente visible
MainActivity -> onStop()
Ya no es visible para el usuario. Aquí puedes liberar recursos pesados que no necesitamos.
SeconActivity -> onCreate y onResume()

El viaje de vuelta: cuando cierras la segundaActivity

cuANDO EL USUARIO DECIDE VOLVER ATRAS, YA SE HA LLAMADO A FINISH, ANDROID DESHACE LOS PASOS ANTERIORES DE FORMA ORDENADA, VAS VOLVIENDO ATRAS PERO NO PUEDES IR HACIA DELANTE, liberandose memoria
SecundActivity se despedie, ejecuta onPause -> onStop -> onDestroy. Android elimina completamente la pila y libera su memoria.

##Preservación del estado
Lo que se ocnserva automaticamente
Texto en EditText
SxcrollPosition
Variables de instancia
Estado de vistas
PERO sin embargo si android necesita liberar memoria por presión del sistema, puede destruirMainActivity mientras está en segundo plano, para esos casos, usa onSabeInstanceState()

Puntos clave para recordar
La pila es real, cada activity que abres se apila encima de la anteiror, contorlar esto es clave para la buena UX y gestión de la emmoria
El cliclod e vida es automático, android llama a los métodos del ciclo de vida por ti. Tu trabajo es sobreescribirlos cuando necesites compoertamientos especificos
El estado dse preserva. Main Activituy se mantiene pero usa onSaveInstanceState para casos criticos
Finish es tu aliado, usadolo estrartegicamente para contorlar que activities permanecen vivas yu uales deben desaparecer