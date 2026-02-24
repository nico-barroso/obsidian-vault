---
tags: [rag, ia, llm]
category: Frameworks
related: [[OpenAI API]]
---

# RAG

**Retrieval Augmented Generation**

Técnica que combina búsqueda de información con generación de texto.

## Funcionamiento

1. **Dividir** documentos en chunks (por límite de contexto)
2. **Embeddings**: Convertir chunks en vectores numéricos
3. **Retrieval**: Buscar chunks similares a la query
4. **Generación**: Enviar contexto + pregunta al LLM

## Uso

```python
# 1. Crear embeddings de documentos
# 2. Buscar chunks similares
# 3. Enviar al LLM con el contexto encontrado
```

> Ver: [[OpenAI API]]
