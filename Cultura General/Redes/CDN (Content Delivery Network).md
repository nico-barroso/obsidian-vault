
| Concepto Clave   | Nota Útil                                                                            |
| :--------------- | :----------------------------------------------------------------------------------- |
| **Definición**   | Red distribuida de servidores que entregan contenido según la ubicación del usuario. |
| **Objetivo**     | Reducir la latencia y la carga en el servidor de origen.                             |
| **Servicio AWS** | [[Amazon CloudFront]]                                                                |

## Definición
Una **CDN (Red de Entrega de Contenidos)** es un sistema distribuido globalmente de servidores de caché. Su función principal es acercar el contenido al usuario final para minimizar el retraso (latencia) en la carga de una web o aplicación.



## Funcionamiento Básico
1.  **Origen:** Tienes tu contenido original en un servidor central (ej. un Bucket [[Amazon S3]] o una instancia [[EC2]]).
2.  **Edge Locations (Ubicaciones de Borde):** Servidores de la CDN repartidos por todo el mundo.
3.  **Caché:** Cuando un usuario solicita un archivo:
    * Si es la primera vez, la CDN lo pide al Origen y guarda una **copia local**.
    * Las siguientes veces, la CDN entrega la copia desde el servidor más cercano al usuario, sin molestar al origen.

## Tipos de Contenido Acelerado
* **Contenido Estático (Archivos):** Imágenes, vídeos, CSS, JavaScript. Se almacenan copias en caché (es el uso más común).
* **Contenido Dinámico:** Contenido que cambia para cada usuario. La CDN optimiza la ruta de red para llegar antes al origen (no siempre se puede cachear, pero sí acelerar el transporte).

## Ventajas Principales
1.  **Mejora del Rendimiento:** Menor latencia porque la distancia física de los datos al usuario es menor.
2.  **Escalado y Disponibilidad:** Al entregar copias locales, se reduce drásticamente la carga de tráfico en el servidor de origen.
3.  **Seguridad:** Actúa como primera barrera de defensa contra ataques (como DDoS).

## Relacionado
- [[Latencia]]
- [[Amazon CloudFront]] (Implementación de CDN en AWS)
- [[Amazon S3]] (Origen común para estáticos)