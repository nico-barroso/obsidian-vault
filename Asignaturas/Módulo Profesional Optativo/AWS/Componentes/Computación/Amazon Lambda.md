Es un servicio serverless, nos permite ejecutar codigo sin levantar servidores
El servidor no se configura,m noc reamos nignuna instancia ec2, amazon proporciona el servidor donde se ejecvuta, solo nos preocupamos de cargar el código, se depsliega en la función y solo se paga por el cómpuito que utiliza (solos e ejecuta cunado se activa)

Arquitectura con ecw
se basa en servidores aprovisionados
necesitas, crear configura ry mantener
escalado manual o semitatomatico
pagas por la ejecución de la instancia, esté activa la app o no
adecuado para palciaciones de larga duracióin, serrrvicio de carga estable , control total
arquitectura se4rverless 
noa dministrras servidores
soplo subes el codigo, no hayu SO ni isntanciuas
Escalado automatico por ewvento
Pagas solo por invocar y tiempod e ejecución reral
Ideal para procesos event dreiven
cargas variables o impredecibles
microservicios o funciones


odemos invocarla desde terminal pero las fuentes de eventos pueden ser invocadas las lambdas desade cualquier otro servicio como amazon s3, si por ejemplo havcemos algo en un bucket, se dispara la fguncion lam,b

configuracion de una configuracion
el codigfo de la funcion
las dependencias (bibliotecas de codigos etc
y elr ol de ejecucion)
Se le puede pasar a amazon cloudweatch para moinitoprea

Ejemplo super tipico: tenemos unas isntancias en ec2 y solo funciona en la franja laboral, perop desde las 8 de la noche hasta la s8 de la mañana delk dia siguiente sigue consumiewndo, podmeos crear una funcion lambda con dos disparadores, en funcion del tiempo cuando llegue a. las 8 es que detenga las instancias que sobran y a las 8 se lanza otro evento quew arranca la instancia, ahorrando costes

eN ENTORNOS DE DESARROLLO, DONDE SE ESTÉ DESARROLLANDO SE PUEDEN USAR LAMBDAS PARA QUE SE DETENGAN TODA SLAS ISNTANCIAS POR LA NOCHE (CUANDO NO SE ESTA TRABVAJANDO)

CUOTAS LIUMITES POR REGION: SIMUTLANEAS SON 1000 ALMACENAMIENTO Y FUNCIONES 75GB