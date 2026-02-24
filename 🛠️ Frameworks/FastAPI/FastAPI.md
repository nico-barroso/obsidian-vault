---
tags: [fastapi, python, api, framework]
category: Frameworks
---

# FastAPI

Framework Python moderno y rápido para crear APIs REST.

## Características

- **Alto rendimiento** (similar a Node.js y Go)
- **Documentación automática** (Swagger UI)
- **Validación automática** de datos (Pydantic)
- **Type hints** integrados

## Ejemplo básico

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    name: str
    price: float

@app.get("/")
def root():
    return {"message": "Hola FastAPI"}

@app.post("/items/")
def create_item(item: Item):
    return item
```

## Temas

- [[Type Hints]] - Type hints en Python

> Relacionado: [[Python]]
