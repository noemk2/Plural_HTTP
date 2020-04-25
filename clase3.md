# HTTP connections

# intro

en el modulo anterior miramos los mensajes HTTP y vimos ejemplos del comando
textual que fluia entre el cliente y el servidor en una transaccion HTTP
pero
Como se mueven esos mensajes realmente
a traves de la red?

Cuando se abren las conexiones de red?

Cuando se cierran las conexiones de red?

Esos son los tipos de preguntas que responderemos en este
modulo ya que consideramos HTTP desde una perspectiva de nivel inferior
Vamos a ver los protocolos de red como el protocolo de control
de transmision y usar una herramienta para analizar la red durante
una transaccion HTTP.
Tambien vamos tener una idea de como podria ser escribir el codigo
en un navegador web que realiza una HTTP request

# whirlwind networking

para comprender las conexiones HTTP tenemos que saber un poco sobre
lo que ocurre en las capas debajo del HTTP
Los protocolos de comunicacion de red los elementos que mueven la informacion
por internet son como la mayoria de las app comerciales

Consisten en capas y capas en una pila de comunicaciones es reponsable de un numero
especifico y muy limitado de responsabilidades
Por ejem HTTP es lo qeu llamamos un protocolo de capa de aplicacion
porque
permite que 2 aplicaciones se comuniquen a traves de la red

Muy a amenudo una de las aplicaciones es un navegador y la otra aplicacion es
servicio web (apache) como IAS o apache
vimos como los mensajes HTTP le permiten al navegador solicitar recursos del
servidor
Pero esas especificaciones HTTP no dicen nada acerca de como los mensajes
realmente se mueven a traves de la red y llegan al servidor

Ese es el trabajo de los protocolos de capa inferior
Un mensaje de una navegador web debe viajar a traves de una serie de capas y cuando
llega al servidor web, viaja a traves de una serie de capas para llegar al proceso
del servidor web
Entonces
la capa debajo de HTTP es lo que llamamos un protocolo de capa de transporte
La mayoria de todo el trafico HTTP viaja a traves de TCP
que es la abreviatura de protocolo de control de transmision
aunque
tecnicamente no es requerido por HTTP
cuando un usuario escribe una URL en el navegador
el navegador 1ero tiene que extraer el nombre de host de la URL y el numero de puerto
si hay alguno ...
Luego
Abre un socket TCP
Especificando esa direccion del servidor
que se derivo del nombre de host y el puerto
que como vimos se configura de manera predeterminada en el puerto 80
y luego
comenzara a escribir datos en el socket
De hecho, vamos a ver el codigo que hace esto en un momento
Capa | comunicacion
Aplicacion | HTTP
Transporte | TCP
Network | IP
Todo lo que el navegador debe preocuparse es escribir el mensaje HTTP correcto en el
socket
La capa TCP acepta esos datos
y
garantiza que los datos llegen al servidor sin perderse ni duplicarse
TCP reenvia automaticamente cualquier informacion que pueda perderse en transito
La aplicacion no tiene que preocuparse por eso
y
es por eso que TCP se conoce como un protocolo confiable

Ademas de esta deteccion de errores
TCP tambien proporciona control de flujo
lo que significa que
TCP se asugurara de que el emisor no envie datos demasiado rapido
para que el receptor procese esos datos
El control de flujo es muy importante en este mundo donde tenemos diferentes tipos
de redes y dispositivos
Entonces
en resumen
TCP proporciona muchos de los servicios vitales que necesitamos para la entrega exitosa
de mensajes HTTP
pero
lo que hace de forma transparente y la mayoria de las aplicaciones
no necesitan preocuparse por TCP en absoluto
simplemente abren el socket y escribir datos en el e
Pero TCP es solamente la primera capa debajo de HTTP

Despues de TCP en la capa de transporte viene la IP
IP es la abreviaruta de protocolo de protocolo de internet
Y asi
mientras que TCP es responsable de la deteccion de errores
control de flujo y confiabilidad general

IP es el responsable de tomar piezas de informacion y moverlas a traves de todos
los conmutadores
enrutadores, puertas de enlace, repetidores y todos estos otros
dispositivos que mueven informacion de una red a la siguiente
y en todo el mundo
IP trata de entregar los datos en el destino
pero
no garantiza la entrega, ese es el trabajo de TCP  
para hacer su trabajo
IP
requiere que las computadoras requieran una direccion que es la
famosa direccion IP
seria 208.192.32.40
esa es la direccion IP de la version cuatro
IP tambien es responsable de
dividir los datos en paquetes que aveces los llamamos datagramas y algunas veces necesitan fragmentar y volver a ensamblar
Esos paquetes para que esten optimizados para un segmento de red particular
Ahora
todo lo que hemos hablado hasta ahora ocurre dentro de una computadora
pero
eventualmente esos paquetes IP tienen que viajar
sobre
un cable o cable de fibra optica o red inalambrica
o
sobre un enlace satelital
y esa es la responsabilidad de
la capa de enlace de datos (Data link)
Una opcion comun de la tecnologia es
Ethernet
con ethernet estos paquetes de IP se convierten en frames y protocolos como Ethernet se vuelven muy enfocados en unos y ceros y señales electricas
Ahora
eventualmente esa señal llega al
servidor y llega a traves de a trajeta de red donde el proceso
se invierte

La capa de enlace de datos entrega el paquete a la capa de IP
que lo transfiere a TCP
que puede reensamblar los datos en el mensaje HTTP original enviado por el cliete
y 
finalmente empujarlo en el proceso del servidor web
Es todo un trabajo maravillosamente diseñado
Todo es posible por estandares

# Programing Sockets

Pense que seria interesante escribir una pequeña aplicacion C que se comporta como un navegador web
en el sentido de que voy
