---
tags: [python, strings]
category: Programacion
related: [[Stringd]], [[Operadores]]
---

# Formateo

## %-formatting

```python
%s  # Strings
%d  # Integers
%f  # Floating point numbers

print("Mi nombre es %s %s" % (name, surname))
```

## .format()

```python
print("Mi nombre es {} {} y mi edad es {}".format(name, surname, age))
print("Mi nombre es {0} {1}" .format(name, surname))  # Por índice
```

## F-strings (Python 3.6+)

```python
name = "Brais"
age = 35

print(f"Mi nombre es {name} y mi edad es {age}")
print(f"Mi nombre es {name.upper()}")  # Con funciones
```

> Ver también: [[Stringd|Desempaquetado de strings]]
