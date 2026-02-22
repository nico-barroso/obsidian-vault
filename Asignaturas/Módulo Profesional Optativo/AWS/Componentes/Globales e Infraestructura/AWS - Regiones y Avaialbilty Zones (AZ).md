Son **ubicaciones geográfica física** independientes en el mundo (ej. `us-east-1` en Virginia, `eu-west-1` en Irlanda).

- **Aislamiento:** Cada región está totalmente aislada de las demás (física y lógicamente). Si una región entera cae (muy raro, ej. catástrofe natural masiva), las otras siguen operando.

- **Soberanía de datos:** Los datos que guardas en una región **NUNCA** salen de ella a menos que tú los muevas explícitamente.

## 2. Criterios para elegir una Región

Al empezar un proyecto en AWS, el primer paso en la consola siempre es elegir la región (esquina superior derecha). ¿Cómo decides cuál usar? Debes balancear estos 4 factores:

### ⏱️ 1. Latencia (Proximity)

- **Regla:** Elige la región más cercana a la **mayoría de tus usuarios finales**, no necesariamente a ti.
- _Ejemplo:_ Si estás en Madrid pero tus clientes están en Nueva York, usa `us-east-1` (Virginia), no `eu-south-2` (España).
- **Herramienta:** Puedes usar sitios como _CloudPing.info_ para medir la latencia desde tu navegador a las regiones de AWS.


### 💰 2. Precio (Cost)

- **Realidad:** El hardware y la electricidad no cuestan lo mismo en todo el mundo.
- **Diferencia:** Las regiones más antiguas y masivas (como `us-east-1` N. Virginia o `us-west-2` Oregon) suelen ser **más baratas**. Regiones como São Paulo (`sa-east-1`) o algunas de Europa pueden ser más caras por impuestos y costes locales.

### ⚖️ 3. Compliance (Soberanía de Datos)

- **Legal:** Si trabajas con datos sensibles (banca, salud, gobierno), las leyes locales (como el **RGPD** en Europa) pueden obligarte a que los datos _nunca_ salgan físicamente del país o continente.
- _Caso:_ Una empresa pública española probablemente te exija usar la región de España (`eu-south-2`) o al menos dentro de la UE.

### 🛠️ 4. Disponibilidad de Servicios (Service Availability)

- **Importante:** **NO** todos los servicios de AWS están en todas las regiones.
- **Innovación:** Los servicios nuevos (ej. AWS Bedrock para IA, o tipos específicos de instancias EC2) siempre se lanzan primero en `us-east-1`. En regiones más pequeñas o nuevas, es posible que algunos servicios tarden meses o años en llegar.