---
tags: [openai, ia, api]
category: Frameworks
related: [[RAG]]
---

# OpenAI API

API para interactuar con modelos de OpenAI (GPT-4, etc.).

## Uso básico

```python
import openai

response = openai.ChatCompletion.create(
    model="gpt-4",
    messages=[
        {"role": "system", "content": "Eres un asistente útil."},
        {"role": "user", "content": "Hola, ¿cómo estás?"}
    ]
)
```

## Modelos

- **GPT-4**: Más potente
- **GPT-3.5 Turbo**: Más rápido y barato

> Ver: [[RAG]] para Retrieval Augmented Generation
