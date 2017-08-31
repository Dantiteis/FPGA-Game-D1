# TOUCH

## Integrantes del equipo de trabajo:

### 1 Daniel Alejandro Rodríguez Chávez daarodriguezch@unal.edu.co

### 2 Nombre1 nombre2 apelido1 apellido2 correo@electronico

### 3 Nombre1 nombre2 apelido1 apellido2 correo@electronico


## Descripción general del sistema: (tomado del documento de clase)

El sistema cuenta con un sensor de Ultrasonido: HC-SR04, el cual funciona hasta una distancia de 4 metros, según el "datasheet", además opera a una frecuencia de 40kHz, la cual resulta siendo de la onda del sonido enviado. El funcionamiento a grandes rasgos es un pulsoque se le entrega al sensor para que funcione, y habrá uno de vuelta por parte del sensor al recibir la señal del ultrasonido; hay un conteo hecho entre dichos pulsos y un cálculo que "traduce" el conteo en un valor óptimo el cual resulta siendo el valor de la distancia que realmente requerimos. El dispósitivo de pantalla táctil (Touch Screen) será conectado con I2C, por cuestiones de prudencia con el precio, no está definido el dispositivo exacto, aunque hay idea con el tipo capacitivo. 

## Descripción de la caja Funcional  (in/out)

Para el Ultrasonido hay 3 cajas principales del sistema: el sensor, un contador y uno que llamamos "traductor". El sensor tiene una única entrada/salida. El contador tiene por entradas P, S, Tr y el "clock" y por salidas están Ten, Tm y un bus T de m conexiones. El que llamamos traductor, porque "traduce un valor de tiempo en distancia" (pero en otros términos hace cálculos de un valor adecuado que los otros bloques puedan usar), tiene por entrada f, Tro, Ten, Tm y el bus T, y por salidas tiene i de n conexiones, Ren, un bus R de k conexiones, Rm, Tr y P.

Para la pantalla táctil, El bloque se simplifica al dispositivo mismo el cual lleva el I2C como protocolo con el procesador, por ende las salidas y entradas únicamente podemos decir que son el SDA y el SCL, las cuales la primera, resulta siendo entrada/salida, mientras la segunda, solo entrada para el bloque de la pantalla táctil (Touch Screen).

## Descripción funcional:

Para el caso del sensor ultrasonido, Tenemos una entrada f desde el procesador de un pulso, para dar la orden para el funcionamiento del bloque completo. Esto más tarde llegará al sensor, pero habrá una salida Rm desde el que llamamos "traductor" la cual, desde un inicio habría estado en 1, para poder permitir dicha orden, en caso contrario diría que "está ocupado", donde su valor es 0. Hacia el contador ocurre algo similar, habrá una variable P que es mandará el mismo pulso pero para esto una entrada Tm deberá estar en 1 para poder permitir dicho acto, luego de mandarlo pasará a 0 para decir que está ocupado. S terminará de mandar el pulso y el contador empezará a funcionar (contar)  con el ciclo de reloj hasta recibir el pulso de vuelta. Una salida Ten será 1 si recibe el pulso de vuelta (y el contador dejará de contar), la cual será para decir que el dato está listo para ser enviado al "Traductor", y esta se enviará por T, un bus de m cantidad de conexiones. El contador habrá de recibir una variable Tr=1 para tener la especificación que el dato fue recibido por el traductor y este último hará los cálculos pertinentes para "traducir" el tiempo de conteo en "longitud de recorrido de la onda", dividiendo en 2 y todo (que sería la distancia total) y una vez tenga ese dato, la variable Ren será 1 para decir al procesador que el dato está listo, el cual se envía por R, un bus de k cantidad conexiones, así como mandará un valor i de n dígitos, el cual será el número propio que identifica al bloque general del sensor, y de vuelta a la vez esperará un valor Tro para entender que el dato se reinició y poder habilitarse para poder volver a recibir la orden de un pulso que requiera el sistema.

Para el caso de la pantalla táctil. La entrada/salida SDA será quien trasmita datos y el SCL será el reloj que la pantalla táctil irá recibiendo.

## Descripción Estructural:

Para el caso del ultrasonido, habrá 3 bloques, como se dijo antes, el sensor, el cual manda y recibe una señal de ultrasonido, está el contador, el cual cuenta el tiempo en ciclos de reloj que toma la señal de pulso de vuelta en regresar, usando un "clock", sin embargo es "asíncrono" como "síncrono", puesto que, aunque una de sus partes prioritarias funciona con reloj, su funcionamiento de comunicación realmente depende de los valores de entradas y salidas de "estado" con el otro bloque. Está el traductor, el cual "traduce" la señal de "tiempo" en "distancia" (hace cálculos), es puramente asíncrono. 

## Diagrama de Estados:



## Arquitectura del periférico:

XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX

## Diagrama de bloques del periférico:

XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX

## referencias:

XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX

