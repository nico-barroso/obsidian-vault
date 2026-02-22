El formato es **MAJOR.MINOR.PATCH** — por ejemplo `2.4.1`:

- **MAJOR** → cambios que rompen compatibilidad ("breaking changes")
- **MINOR** → nueva funcionalidad compatible con lo anterior
- **PATCH** o **hotfix** → corrección de bugs, sin cambios funcionales

> Ejemplo: pasar de `1.3.2` → `2.0.0` implica que algo del API o comportamiento cambió y puede romper integraciones existentes.

Dato curioso, muchas veces se llama al hotfix o shame

---

## Versionado por Fecha (CalVer)

Formato basado en la fecha de lanzamiento: `YYYY.MM.DD` o variantes. Común en sistemas operativos como Ubuntu (`24.04`) o herramientas de infraestructura.

---

## Etiquetas de madurez

Más allá del número, se usan sufijos para indicar el estado:

|Etiqueta|Significado|
|---|---|
|`alpha`|Inestable, en desarrollo activo|
|`beta`|Funcional pero puede tener bugs|
|`RC` (Release Candidate)|Candidato a producción, en pruebas|
|`stable` / `GA`|Listo para producción|
|`LTS`|Soporte extendido (Long Term Support)|
|`deprecated`|Aún funciona pero no se recomienda|
|`EOL`|Sin soporte, no usar|

---

## Buenas prácticas

- **Nunca bajar de versión** sin comunicarlo explícitamente.
- **Changelogs claros** para que el usuario entienda qué cambió.
- **Versionar desde el día 1**, aunque el producto sea pequeño.
- En APIs públicas, mantener **retrocompatibilidad** el mayor tiempo posible antes de un MAJOR bump.

---

La clave es que el número de versión sea un **contrato de confianza** con el usuario: que al verlo sepa exactamente qué esperar del cambio.