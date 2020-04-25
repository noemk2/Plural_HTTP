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

# handshakes with a sharkwire

# On the evolution of HTTP

En los primeros dias de la web cuando teniamos la especificacion HTTP original
la mayoria de los recursos eran textuales
y
salia con su computadora y solicitaba un documento de un servidor web
El servidor web se lo devolvia a usted y
usted podria apagarse y leerse durante cinco minutos
antes de que tal vez haga clic en un enlace en ese documento y solicite otro

El mundo era muy simple entonces
y era muy facil para un navegador abrir una conexion a un servidor
enviar una
solicitud, recibir la respuesta y luego cerrar la conexion
La idea era
Por que mantenemos las conexiones abiertas si solo las necesitamos una vez cada cinco minutos

Pero la web de hoy en dia la mayoria de las paginas web requieren
mas de un recurso para procesar por completo
Cada pagina web que voy a tener
va tener una o mas imagenes
uno o mas archivos javascript, uno o mas hojas de stilo css
no es raro solicitar una pagina web y tener que generar 30 50 o 100 solicitudes HTTP
adicionales para recuperar todos los recursos asociados con
esa pagina
entonces
si los navegadores web acuales abrieran conexiones de una en una como esta y esperaran a que
cada recurso se descargue completamente antes de comenzar la proxima descarga
entonces
la web se setiria muy lenta porque la senal de internet es muy larga recorre distancias y se
abre paso a traves de diferentes piezas de hardware y como vimos en wire shark
tambien hay algo de sobrecarga en el establecimiento de una conexion TCP  
el saludo de 3 pasos

en promedio una pagina web hacer 120 solicitudes HTTP

# parallel connections

la mayoria de los agentes de usuario
tambien
conocidos como navegadores web
no
realizaran solicitudes de una en una por una
sino
que puede abrir conexiones multiples y paralelas a un servidor
conocidos como navegadores web
no
entonces por ejemplo
la descarga de una pagina html
el navegador puede ver 2 etiquetas de imagen en esa pagina
por lo que puede abrir 2 conexiones para
descargar las imagenes simultaneamente
con suerte
eso reducira
la cantidad de tiempo necesaria para mostrar las imagenes
a la mitad pero no siempre es perfecto
y
la cantidad exacta de conexiones paralelas que hara
un navegador dependera del navegador y de como este configurado

Durante mucho tiepo consideramos 2 como la cantidad maxima de conexiones en  
paralelo que creia un navegador
consideramos 2 el maximo porque el navegador mas popular de cualquier ano es Internet explorer 6
solo permite 2 conexiones simultaneas a un solo host y para ser justos
Internet Explorer 6 realmente solo seguia la especificacion HTTP
que dice un solo usuario cliente no debe mantener mas de 2 conexiones con un servidor
Sin embargo muchas personas encontraron formas de evitar esta limitacion o al menos las limitaciones
percibidas para aumentar la cantidad de descargas paralelas
entonces
por ejemplo
esta limitacion de 2 conexiones es por host por nombre de host lo que significa que IE 6
haria felizmente 2 conexiones a www.odetocode.com y 2 conexiones a las imagenes de este host
entonces al alojar imagenes en un servidor diferente
entonces puede tener cuatro solicitudes paralelas y ese servidor diferente solo necesita ser un
nombre de host diferente
En la ultima instancia sus registros DNS podrian senalar las 4 solicitudes al mismo servidor fisico
pero
el IE 6 solo estaba usando ese limite de conexion por nombre de host
felizmente abriria cuatro conexiones en ese escenario
IE 8 permitio conexiones hasta de 6

pero porque no a 100 conexiones paralelas?
es que van a obedecer la ley de rendimientos decrecientes
si tiene demasiadas conexiones abiertas puede saturar y congestionar la red
especialmente cuando se trata de dispositivos moviles y redes no confiables
Por lo tanto
tener demasiadas conexiones puede danar el rendimiento y tambien un servidor solo puede
aceptar un numero finito de conexiones
entonces
si
100000 navegadores crean simultaneamente 100 conexiones a un solo servidor web
estoy seguro de que van a suceder cosas malas
Aun asi usar mas de una conexion por agente es mejor que descargar todo de manera serial
y las conexiones paralelas

# Persistent Connections

al principio era facil para un navegador web abrir y cerrar conexion a un servidor
y que literalmente craba un nuevo socket
lo conextaba enviaba una solicitud
optenia una respuesta y se cerraba la toma
Eso estaba en linea con la idea de HTTP de ser un protocolo completamente sin estado

Pero
como hemos visto el numero de solicitudes por pagina ha crecido y la sobrecarga generada por
para reducir esto
http 1.1
suguiere conexiones persistentes
y de hecho las conexiones son el tipo de predeterminado de conexion en http 1.1
una conexion persistente permanece abierta despues de completar una transaccion de respuesta
de
solicitud
eso deja al navegador con un socket ya abierto que puede usar para continuar haciendo solicitudes al
servidor sin la sobrecarga de abrir un nuevo socket
las conexiones persistentes tambien evitan la estrategia de inicio lento
que es parte del control de congestion TCP y que hara que las conexiones persistentes tengan un mejor
rendimiento a lo largo del tiempo
Asi que en resumen estas conexiones persistentes que tenemos hoy con HTTP
generalmente reducen el uso de memoria
reducen el uso de CPU , reducen la congestion de red, reducen la latencia
generalmente mejoran el tiempo de respuesta de una pagina, pero como todo en el software siempre hay un incoveninente
Un servidor solo puede admitir un numero finito de conexiones el nuemro exacto depende de la cantidad de memoria
la configuracion del servidor y el rendimiento de su aplicacion
hay un gran cantidad de variables alli

Por lo tanto es dificil dar un numero exacto pero en terminos generales
si esta hablando de soportar miles de conexiones concurrentes
tendra que comenzar a probar para ver si
un servidor admite esa carga
Muchos servidores estan configurados para limitar el numero de conexiones simultaneas muy por debajo del punto donde el servidor
simplemente se caera
y esa configuracion es tanto una medida de seguridad como
cualquier otra cosa
Ayuda a prevenir un ataque de servicio de denegacion porque es relativamente facil para alguien crear un
programa o un script que solo abrira miles de conexiones persistentes a un servicidor y no hara nada con ellos
o enviara una cantidad minima de tados a traves de las conexiones
Por lo que las conexiones
persistentes son la optimizacion de rendimiento
pero algunas personas tambien las ven como una vulnerabilidad
entoces
pensando que esas linesas de conexiones persistentes posiblemente sean una vulnerabilidad
hemos hablado de que permanezcan abiertas pero
por cuanto tiempo
en un mundo en el que tiene escalibilidad infinita
puede mantener las conexiones abiertas todo el tiempo que desee
pero
dado que un servidor admite un numero finito de conexiones
la mayoria de los servidores se configuran para cerrar
una conexion persistente si esta inactiva
durante un perioto de tiempo

# pipeline conection (tuberia)
un usuario puede enviar multiples solicitudes HTTP en una sola conexion y enviarlas antes incluso de esperar la primera
respuesta
pipelig permite empaquetamiente mas eficiente de solicitudes y paquetes y puede reducir la laetencia pero como digo simplemente no
es tan ambpliamente soportado como las conexiones paralelas y persistentes
