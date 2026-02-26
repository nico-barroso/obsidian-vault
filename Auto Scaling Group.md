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

Auto Scaling Group Politicas de escalado dinamico
Escala de siguimeinto de objeticos
lo mas sencillo
Escalado simple/escalonado cundos e active una alarma de cloudwatch, añlade 2 unidades

Acciones programatas Anticipa un escalado basado en patrones de uso conocidos (ej en el baclkfriday añadimos 5 mas porque se que va a haber mucha. mas gente. tambien se puede subir la capaicdad minima, la deseada etc

)
Escalado predictivo: previsión continua de la carga y proigramacion del escalado por adelantado 
buenas metricas para escalar
CPUUtilization Utilizacion media de la cpu en tus instancias
RequestCountPeeTarget para asegurarse de que el numero de peticiones por isntancias EC2 es estable
Promedio de entrada/salida de red si tu app esta vinculad

Auto Scaling Groups
Despues de que se produzca una actividad de escalado estaras en periodo de enfriamiento (defecto 300 segundos)
durante ese periodo el ASFG no lanzara ni terminara instancias adficionaels


Politicas de escalado
Escalado automático Actualizacion de instancia
Objetivo actualizar la plantilla de lanzamiento y luego volver a crear todas las instancias ec2
Para ello podemos utilizar la función nativa de actualizacion de isntancia
Establece el porcentaje minimo de salud
Podemos especificar el tiempo de "warming" que es cuanto tiene que estar activa la instancia para que funcione