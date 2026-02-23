
| **Concepto Clave**         | **Nota Útil**                                                          |
| -------------------------- | ---------------------------------------------------------------------- |
| **Integridad Estructural** | El número de separadores (comas) define las columnas, haya datos o no. |
| **Dato Vacío**             | Se representa con dos comas consecutivas `,,`.                         |
| **Universalidad**          | Cualquier parser estándar cuenta las comas para asignar índices.       |

#### 1. La Regla de la Estructura Rígida

El formato CSV (_Comma Separated Values_) no es autodescriptivo por registro; depende totalmente de la posición.

- Si la cabecera define 5 columnas, **cada fila** debe respetar esa estructura implícita.
    
- Si falta un dato, no se omite la columna: se deja el espacio en blanco delimitado.
    

#### 2. Representación de Vacíos

Cuando un campo no tiene valor (`null` o cadena vacía):

- **Visualmente:** Aparecen dos comas seguidas `,,`.
    
- **Interpretación:** El parser lee una cadena de longitud 0 (`""`) entre esos delimitadores.
    

#### 3. Ejemplo Práctico

Supongamos la estructura: `ID, Nombre, Teléfono, Ciudad`

|**Caso**|**CSV Raw (Texto Plano)**|**Interpretación**|
|---|---|---|
|**Datos Completos**|`1,Ana,600111222,Madrid`|Todos los campos tienen valor.|
|**Falta Teléfono**|`2,Luis,,Barcelona`|El parser asigna: ID=2, Nombre=Luis, **Tlf=""**, Ciudad=BCN.|
|**Falta Ciudad (Final)**|`3,Eva,600333444,`|La coma final es obligatoria para indicar que la columna existe pero está vacía.|

#### 4. Implicación en el Algoritmo (Java)

En nuestro `CsvUtils`, la lógica actual ya soporta esto:

1. Al encontrar una coma (`else if (ch == ',')`), guardamos lo que hay en el `StringBuilder`.
    
2. Si entre la coma anterior y la actual no había nada, el `StringBuilder` está vacío.
    
3. Se añade un `String` vacío (`""`) a la lista. **Esto es correcto**.
    

> ⚠️ Cuidado con String.split():
> 
> En Java, el método nativo line.split(",") descarta por defecto los campos vacíos si están al final de la línea.
> 
> Por eso es mejor usar nuestro parser manual CsvUtils, que controla explícitamente cada delimitador.

---

### Metadatos y Organización

**Lista de enlaces sugeridos:**

- [[Java - Proyecto Parser CSV Genérico]]
    
- [[Java - Clase String]] (Manipulación de cadenas)
    

Tags recomendados:

#csv #estandar #formatos #algoritmos #data_structure
