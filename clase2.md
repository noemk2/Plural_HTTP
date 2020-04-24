#HTTP Messages
signal transmitted message received

vamos a ver los mensajes internos dentro de una comunicacion HTTP
veremos
metodos
tipos de mensajes
encabezados HTTP
codigos de estado

podran deectar problemas y depurar problemas cuando las app web no funcionen

#tipos de mensajes

una metafora
en una aeropuerto una persona pregunta a otra Que hora es?
Para que esa persona responda con la hora exacta
algunas cosas tienen que estar en su lugar

1. la persona que ha solicitado debe comprender su pregunta (si no sabe ingles, es posible que no pueda responder)
2. la persona a la que ha solicitado tendra acceso a un reloj o a algun tipo de dispositivo de cronometrae

Esto es algo similar como funciona HTTP

Usted el cliente y necesita un recurso de otra parte el recurso es la informacion sobre la hora del dia
entonces haces una solicitud a la otra parte, usando un lenguaje y vocabulario que entiendes
y esperas que tambien lo haga
Si la otra parte entiende su solicitud y tiene el recurso disponible
puede responder
Si no entiende la solicitud es posible que no obtengas ninguna respuesta
La especificacion HTTP

La especificacion HTTP/1.1
especificacion: define el idioma, para que todos en la web, todos los clientes y todos los servidores
puedan entenderse entre si
Define los mensajes que se intercambian en la web y como deberian ser y que contienen

Y resulta que hay 2 tipos de mensajes
HTTP es un protolo de solicitud y respuesta por lo que el primer tipo de mensaje es la solicitud HTTP
(HTTP request este es el primer mensaje)
Eso es lo que envia el cliente al servidor y formatean cuidadosamente ese mensaje para que el servidor
lo entienda
Un servidor responde utilizando un tipo diferente de mensaje
El segundo tipo de mensaje que es un respuesta HTTP (HTTP response)
Y nuevamente ese mensaje sera formateado para que el cliente lo entienda
Esta formateado de acuerdo con HTTP/1.1 especificacion
La solicitud y la respuesta son 2 tipos de mensajes diferentes, pero se intercambian dentro de
una solo transaccion HTTP (A single HTTP transaction)
Los estandares definen que se incluye en esos mensajes
de modo que todos lo que hablan HTTP se entiendan entre si y puedan intercambiar recursos

O bien cuando el recurso no existe, la respuesta HTTP puede contener un mensaje de error
que el cliente entendera si existe

# A manual request

Un navegador web sabe como enviar una solicitud HTTP abriendo una conexion de red a un servidor
o maquina y enviando ese mensaje de solicitud

Por ejem
Si hacemos una solicitud con url http encoding al servidor odetocode.com y con un path hacia una imagen jpg
el broweser hace esa solicitud y muestra el jpeg

tenga en cuenta que una cosa que sucedio aqui es la
url cambia de www a simplemente odetocode.com/odetocode.jpg

No hay nada magico sobre esta solicitud
Es solo un comando en texto ASCII simple
y
esta formateado segun la especificacion HTTP
y cualquier aplicacion que pueda enviar datos a traves de la red

Practicamente cualquiera de esas aplicaciones puede realizar una solicitud http
Incluso puede hacer una solicitud manualmente usando una app como telnet
desde la linea de comando

Telnet es una applicacion muy antigua
\$ telnet odetocode.com

el problema es que telnet de forma predeterminada intenta usar ele puerto 23
y no hay nada escuchando el puerto 23 en odetocode.com
el puerto predeterminado es el 80
esto nos conecta

Veamos si el servidor entiende los mensajes de texto sin formato
puedo optener una imagen jpg?
esto nos marca un error 400 hisite una mala solicitud http
PERO recivo una respuesta

\$ telnet odetocode.com 80
GET verbo que es lo quiero hacer
GET /odetocode.jpg el recurso al quiero acceder
GET /odetocode HTTP/1.1 El protocolo que estoy usando
en la siguiente linea colocamos informacion adicional que se requiere en cada mensaje
Host: wwww.odetocode.com es el host a cual quiero conectarme

el servidor realmente no sabe que estoy tratando de conectarme a odetocode.com
auque lo escribi en la ventana de comandos

eso tiene que estar en el mensaje Tiene que analizar eso y descubir a donde enviar
este mensaje que sitio entonces con todo eso en su lugar puedo presionar

recibimos un respuesta
URL cononicaclization

bueno si hacermos el llamado bien sin wwww en el host
optenemos en este caso la imagen jpg en texto plano

HTTP/1.1 200 OK
Content-Type: image/jpeg
Last-Modified: Sat, 03 Oct 2009 20:09:10 GMT
Accept-Ranges: bytes
Etag: '0f7b5e6544ca1:0'
Server: Microft-IIS/7.0
X-Powered-By: ASP.NET
Date: Sun, 15 Jan 2012 16:14:20 GMT
Connection: close
Content-Length: 11751

-- imagen en texto plano --
linea 109
Mensaje de respuesta HTTP, nos dice que la solicitud fue bien que el contenido que se devuelve
linea 110
Tipos de MIME
linea 111
cuando se modifico este recurso
linea 112

Lo que hemos hecho aqui en la ventana de telnet que es emitir una solicitud para ese JPEG ser
redireccionado, volver a enviar la solicitud a un host diferente y realmente
extraer los datos - eso es exactamente lo que sucedio aqui en el navegador

# HTTP methods

hablemos de la solicitud que envie al servidor en ese ultimo clip
La primera palabra que escribi en la sesion de telnet

GET

get uno de los metodos HTTP principales
Cada mensaje de solicitud debe incluir uno de los metodos HTTP disponibles
Y el metodo le dice al servidor que quiere hacer la solicitud
Asi que obtenga deseos de hacer lo que parece que quiere hacer , quiere obtener o de hecho recuperar un recurso
Puedo obtener una imagen u obtener un archivo PDF
una pagina HTML o cualquier otro recurso que pueda tener el servidor
Algunos de los metodo HTTP comunes se muestran en esta tabla

GET retrive a resource
POST update a resource
PUT store a resource
DELETE remove a resource
HEAD retrive the headers for a resource

los principales son get y post
entonces cuando la especificacion http enumera una cantidad de metodos legales,
incluso mas de lo que vemos aqui las especificaciones HTML solo
usan get y post
Asi que PUT y DELETE casi nunca se usan en aplicaciones web

Ahora si esta escribiendo un servicio web HTTP
es posible que desee utilizar estos otros metodos para agregar y eliminar
recursos, pero debera tener cuidado por que incluso hay algunas tecnologias y piezas
de hardware del lado del servidor en el servidor red que no procesara PUT y DELETE mensajes

Entonces
principalmente lo que usas para hacer el trabajo con HTTP es obtener y publicar
Un browser web emite una solicitud de GET request cuando quiere recuperar un recurso
como una pagina una imagen un video o un documento
Y una solicitud de obtencion (GET) es probable el tipo mas comun de solicitud
Basicamente se usa para leer datos

Un navegador web envia una solicitud posterior (POST request)
cuando tiene datos que desea enviar al servidor para un escenario de actualizacion

Por ejm si voy a amazon.com
y haga clic en agregar al carro, que va emitir una solicitud posterior(POST request) a amazon
describiendo lo quiero comprar
Las solicitudes de envio generalmente generan mediante un elemento de formulario
en una pagina web
como un formulario que completa con los elementos de entrada para la direccion y la informacion de la
tarjeta de credito
Te mostrare algunos escenarios especificos con etiquetas de formulario

# GET and POST scenarios

safe vs Unsafe

Hay una parte de la especificacion HTTP que habla sobre metodos HTTP seguros
Los metodos seguros son metodos que lee y ve los recursos de un servidor web

Los metodos inseguros son metodos que le permiten cambiar recursos en un servidor web

El metodo get es uno de los metodos seguros, ya qeu solo debe recurperar un recurso y no alterar el estado
de ese recurso
Por lo tanto enviar una solicitud de obtencion de una imagen JPEG
no cambia la imagen. Simplemente busca la imagen para mostrar (GET)

Decimos que una operacion de obtencion en la web nunca deberia tener un efecto secundario
en el servidor. Contraste eso con una publicacion HTTP
Este no es un metodo seguro (POST)
Por lo general, cambia algo en el servidor. La publicacion es lo que utilizamos para procesar una transaccion
de tarjeta de credito
actualizar una cuenta enviar una orden o realizar alguna otra operacion que puede ser destructiva o constructiva

Por esta razon los browsers web normalmente tratan el envio y la publicacion de manera diferente, ya que obtener es (GET)
seguro y POST es inseguro

cuando estamos llenando un formulario y actualizamos no pasa nada
es decir es normal si enviamos muliples GET request
pero
cuando rellenamos y enviamos(hacemos un metodo POST)
y actualizamos Sale un warning

El navegador sabe que acabo de realizar una operacion insegura
Estoy tratando de actualizarlo
Y eso podria hacer que presente una transaccion duplicada de tarjeta de credito
Podria tratar de crear dos cuentas, en lugar de una sola

Hay muchos escenarios en los que sucederan cosas indeseables, si hago clic en boton continuar para volver hacer esa operacion

para solucionar este problema de mandar 2 veces al momento de actualizar (cuando sea aya llamado a POST)
seria
si hay una publicacion atras,
no intentemos descubrir como volver a mostrar
esta pagina al usuario

En cambio

guardemos los valores que el usuario ingreso y los colocamos en la base de datos
En este caso voy a ponerlos en un par de variables de sesion del lado del servidor
y esos se implementan con cookies HTTP
que vermos en un modulo
los formularios se guardan en el servidor en un lugar donde pueda obtenerlos
despues de que hayamos respondido
redirigir y redirigir el navegador a una pagina diferente, firmado

dato: cuando accedemos a un pagina el navegador esta solicitando un metodo GET hacia el servidor

es decir guarda en cookies los forms (guardandolo con el post echo)
despues redirige la pagina a una pagina get de sucess
tecnologia: POST/redirect/GET

no todos los forms requieren un metodo post
cuando se usar el metodo igual a publicar
Los valores que estan dentro de aqui se tunelizan en el mensaje HTTP
pero tambien puede tener una forma
metodo igual a obtener y hay una diferencia significativa entre
los dos

cuando lo hacemos con el metodo get en un formulario
lo que va hacer es emitir una solicitud de obtencion(GET request)
a la url action= 'result.cshtml'
y en lugar de tomar la entrada que tengo (mis input)
dentro de este formulario y ponerlas en el cuerpo del mensaje
las colocara en la URL

cuando se utliza un input de type search
la url cambia a result.schtml?q=food
name = 'q'
el metodo get request forzo a colocarlo en la url

# Request messages

una solicitud completa constara de las siguientes partes
[method][url][version]

[headers]

[body]
este mensaje siempre esta en texto ASCII por cierto
las solicitudes de GET normalmente no ve un cuerpo
los encabezados son obligatorios
y tambien generalmente contienen informacion util qu puede ayudar a un servidor
a preocesar una solicitud
Por
estandar para que en el headers incluya las fechas
RFC822 Section 5.1

# Common request headers

header | Description
Referer | The URL of the referring page
User-Agent | Information about the browser
Accept | Preferred media types
Accept-Languaje | Preferred language
Cookie | Cookie information
If-Modiried-Since | Date of last retrieval
Date | Creation timestamp for the message

# response messages

despues de la solicitud debe recibir una respuesta y un mensaje de respuesta
es similar a un mensaje de solicitud
tiene una linea de inicio que incluye una linea de inicio que incluye una
version, que viene primero aqui en la respuesta. Luego, el codigo de estado mas
importante que detallaremos

el body puede ser conenido html o de imagen

respuesta completa de un http

HTTP/1.1 200 OK
Cache-Control: private
Content-Type: text/html; charset=utf-8
Server: Microsoft-IIS/7.0
X-AspNet-Version: 2.0.50727
X-Powered-By: ASP.NET
Date: Sat, 14 Feb 2003 04:00:08 GMT
Content-Length: 11751

<html>
... content ...
</html>

