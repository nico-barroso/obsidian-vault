---
tags: [python, tipos]
category: Programacion
related: [[Operadores]]
---

# Type Hints

Python permite anotar tipos pero **no los fuerza**:

```python
address: str = "Mi dirección"
print(type(address))  # str

address = 32  # No da error, cambia a int
print(type(address))  # int
```

## Para qué sirven

- **Documentación** - Código más legible
- **IDE support** - Autocompletado y errores en tiempo de desarrollo
- **Static analysis** - Herramientas como mypy

```python
def saludar(nombre: str, edad: int) -> str:
    return f"Hola, tengo {edad} años"
```

> Ver: [[Operadores]] para operaciones con tipos
