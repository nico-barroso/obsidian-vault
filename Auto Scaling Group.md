La carga de sitios web puede cmabiar 8netflix no tiene los mismos usuarios en las horas que tocan
En el Cloud, puedes crear y deshacerte de servidores muy rápidamente

El objetivo de un AutoScaling es:

Esquema de como funciona el AutoScaling

Tenemos deifnida la capacidad mínima : 2 ec2 por ejemplo
Luego la capacidad deseada: durante el fin de semana, tendremos 4 instancias de funcionamiento
Y como máximo en caso de excalar, tenemos tres instancias de mas como capacidad máxima

Ayto Scaling Grouop en AWS con Load Balancer el elastic load balancer se puede conectar con esas instancias y comprobar la salud de tus instancias e ec2 en el caso de que estas tengan trafico en 

Escalado automatico con alarmas (clioud watch)

Es posible escalar con cloudwatch
Una alarma monitoriza una metrica (como la cpu media)
las metricas como la cpu media se calculan para todas las instancias del asg
podemos crear politicas de escalado