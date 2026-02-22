Node modules
node trabaja con commonjs
EDSModules usa import/export
mientras que commonjs require/exports

__ dirname
__ filename
Path
Path es un objeto de node con comandos que podemos usar:
path.join(__dirname)

commonjs
```js
const Colors = require(colors.js)

module.export ...
```


fechas
new Date ojo en formato fecha de lado de cliente y de servidor
process.argv -> saca las rutas de los argumentos que ponemos enc onsola al invocar el node

fs -> file sistem

const fs = require('fs/promise4s)
try{
await fs.readir
catch

}


Migraciones
!!!IMPORTANTE
Las migraciones es hjacer las bases de datos a muy poquito y simepre con la popsibilidad de hacer rollback
En la base de datos se creea uan carpeta con diferentes ficheros -[datetame]_filename.js
Cada fichero va a tener un objeto up{} -> para subir migración
y un objeto down{} -> para hacer rollback

La idea es ir registrando en una tabla de control
