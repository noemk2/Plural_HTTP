HTTP es el protocolo que me permite buscar 'hornos de microhornas'
y comprar uno en amazon
Tambien es el protocolo que me permite reunirme con viejos amigos en un chat de facebook
o cuando no hay nada bueno en la television, puedo ir a youtube
y ver videos de gatos haciendo cosas graciosas
HTTP es un protocolo de comunicacion entre cliente-servidor
Protocolo de transferencia de hipertexto

todas estas cosas suceden en la web donde HTTP define lo que es posible

Es un protocolo que permite que un servidor web desde un centro de datos en
USA envie informacion a un cibercafe en Australia
Donde un alumno puede leer una pagina web que describe la dinastia ming en china
En este curso

tener una solida comprension de HTTP

escribir mejores app web y servicios web
puede ayudarlo a depurar aplicaciones y servicios cuando las cosas salen mal

URL
Uniform resorse locator
cuando ingresamos http://www.food.com

el navegador web entiende esa sintaxis http://www.
y sabe que tiene que hacer una solicitud HTTP a un servidor llamado food.com
http://www. esto es lo que llamamos URL (localizador Uniforme de Recursos)

Representa un recurso especifico en la web

En este caso, la URL localiza un recurso que es una pagina de inicio de la fod.com
Un recurso (food.com home page)

cosas con las que quiero interactuar en la web, imagenes, paginas, archivos y videos TODOS estos son recursos

hay miles de millones si no billones de lugares para ir en internet en otras palabras
hay billones de recursos

quisas se encuentre con otros esquemas en internet
como ftp para el protocolo de transferencia de archivos
ftp://server.com/download/tpsreport.pdf

o tambien direcciones de correo electronico
mailto://scott@odetocode.com

porque las URL se usa para otros protocolos ademas de HTTP

estructura

http://food.com/recipe/grilled-cauliflower
http es URL scheme

food.com es Host , literalmente le dice a mi computadora en internet que esta alojando recurso
mi computadora usara de nombre de dominio para buscar una direccion de comida.com, convirtiendolo
en una direccion de red y sabra exactamente donde enviar una solicitud

DNS SERVER(sistema de nombre de dominio)
Q: Where is food.com?
A: Its at IP address 204.78.50.82

tambien puede especificar esa porcion de host usando la direccin IP directamente
pero la mayoria de la gente quiere usar el nombre de dominio

recipe/grilled-cauliflower
La utlima parte de la URL es la ruta URL. La comida.com host debe reconecer que recursos especificos solicitados por esta ruta y
responder adecuadamente

Una ruta se ve muy jerarquica, como una ruta de sistema de de archivos y a veces una URL
apuntara a un recurso real que se encuentra en el sistema de archivos o disco duro del host

por ejemplo, la url comida.com/images/logo.jpg
apuntara a un archivo jpeg que realmente existe en la food.com sorvidor de comunicacion

Sin embargo los recursos tambien pueden ser dinamicos
sin enbargo los recursos tambien pueden ser dinamicos
la comida URL.com/recetas/brocoli
probablemete no se refiere a un archivo real en la food.com servidor
En cambio, se esta ejecutando algu tipo applicacion en food.com host que
tomara esa solicitud y construira un recurso usando contenido de una base de datos

La applicacion puede ser construida usando asp. net php, pearl, ruby on rails, o alguna otra tecnologia web
que sepa como responder a las solicitudes entrates mediante el evio de HTML
que puede mostrar un navegador. De hecho, en estos dias muchos sitios web intentan evitar tener algun tipo de nombre de
archivo real en la url

Para empezar, los nombre de archivo generalmente estan asociados a con una tecnologia espefica
pero muchas URL sobreviran a su tecnologia que se usa para alojarlas y servirlas

En segundo lugar, muchos sitios quieren colocar palabras clave en una URL
como tener receta y brocoli en la url de recursos de receta de brocoli
tener esas palabras clave ene las url es una forma de optimizacion del motor de busquedas qeu clasificara el recurso mas
alto en los resultados del motor de busqueda.

Sus palabras clave descriptivas no son nombre de archivos que son importantes para la URL en estos dias

Algunos recursos tambien llevaran al navegador a descargar recursos adicionales
food.com icluira images, archivos de script, javascript files,css y otros recursos
que combinan para presentar la receta que estamos viendo
Si ve el codigo fuente
HTML es una pagina, vera etiquetas, script, etiquetas de imagenes y etiquetas images, etiquetas de estilo que apuntara a
URL adicionales
Por lo tanto, al compilar una pagina web
como sea un navegador suele hacer multiples solicitudes HTTP para recuperar
todos los recursos necesarios

HTTP and IIS

vamos a hacer una pequeña demostracion
IIS o internet formation services
es el servidor web que puede ejecutar en maquinas con windows

Ports, querys and fragments

una url consiste en
skin que es http://
host que es food.com
path que es /recipes

pero hay una informacion adicional en esta url
es : y el numero 80
representa el numero de puerto que el host va realizar para
escuchar las solicitudes HTTP
El numero de puerto
predeterminado para HTTP es el puerto 80
Por lo tanto, generalmente ve este numero de puerto omitido de una URL
No necesitaria usar colon 80 para llegar a cualquier servidor web que
este escuchando en el puerto predeterminado porque el navegador simplemente sumira que quiere decir puerto 80
que se espefique algo mas
Sin embargo, si entre IAS que tambien escucha el puerto 80 de manera
predeterminada y lo configure para que escuchara el puerto 8080
entonces tendria que poner ese numero de puerto en la URL
para poder llegar a esa prueba
solo necesita especificar el numero de puerto si el servidor esta escuchando
un puerto diferente al puerto predeterminado
esto ocurre mucho en terminos de prueba y testeo

las web comerciales no requiere un numero de puerto
su URL hace que la URL sea mucho mas dificil de recordar y hace que URL sea poco mas larga

Veamos otras URL
http://bing.com/search?q=jaboticaba
Este todabia tiene un esquema y una ruta de host y URL
por supuesto, pero tiene otra pieza opcional
URL shema http://
host bing.com
URL path search
pero
tiene otra pieza adicional que se conoce como query
?q=jaboticaba
se hace en el backend atraves del metodo querystring

#url encoding

todos los desarrolladores de software que trabajan con la web deben conocer los
problemas de caracter y codificacion con las URL
Los estandares oficiales que describen las URL hacen todo lo posible para garancizar que las url sean
tan utilizables e interoparables
como sea posible
Una URL debe debe ser tan facil de comunicar a traves del correo electronico
como colocar una cartelera o una pegatina para el parachoques o una tarjeta de visita
Por este motivo, los estandares para encontrar caracteres inseguros para URL  
y caracter inseguro son los que no deberian aparecer en una URL
Po ejemplo
el caracter de espacio se considera inseguro por que los espacios son dificiles
de leer. Pueden aparecer / desaparecer por leer
(es acaso un espacio o 2)
Pueden aparecer / desaparecer por error cuando la URL esta impresa
Otros caracteres como la libra se usa para delimitar un fragmento
Esto no significa que no puedas usar un signo de libra en una URL
solo significa que el signo de libra solo se puede usar en su posicion reservada
que es delimitar un fragmento

lamentablemente aun puede transmitir caracteres inseguros en una URL pero deben estar codificados
por terminos diferentes. pero es el mismo resultado
La codificacion porcentual es el proceso de tomar un caracter como el caracter de espacio y una URL
y reemplazarlo con una porcentaje (%20)
ejm
Commolnly encoded Values
ASCII character | URL encoding
space %20
! %21

ejemplo
si quieres tener a Scott Allen en una url
necesitarias
http://ps.com/scott%20Allen

los frameword lo haran mas facil ya que tienen api

#Content types

que significa realmente cuando ingresamos a una URL en el navegador que queremos recuperar o ver algun
recurso
Hay una enorme cantidad de materiales para ver en la web y tambien veremos mas adelante como HTTP nos permite
crear eliminar y actualizar recursos pero por ahora nos mantendremos enfocados en la recuperacion
No hemos sido muy especificos sobre los tipos de recursos
que queremos recuperar
Hay miles de recursos diferentes en la web
Hay imagenes , documentos de hipertexto, documentos xml, archivos de video, audio aplicaciones
ejecuciones, documentos pdf y documentos de word

para que un servidor pueda servir correctamente un recurso y para que el cliente muestre correctamente un recurso las
partes involucradas deben ser muy
especificas y precisas sobre el tipo de de recurso
El recurso es una imgagen o una pelicurla ?

no deseariamos que nuestros navegadores web intenten procesar una imagen JPEG como text y no nos gustaria
o que tomen el texto e intenten interpretarlo como una imagen
Entonces, cuando un host responde a una solicitud http
devuelve un recurso y tambien espcifica el tipo de contenido
Esto tambien se conoce como el (content type)

El servidor depende de las extenciones multiproposito de correo de internet o los estandares MIME
Common MIME Types;
type / Subtipe | Description
application/atom+xml | Atom feed
application/json | JSON data
image/gif | GIF Image
image/png | PNG image
text/html | HTML

Aunque MIME se diseno originalmente para comunicaciones por correo electronico
funciono tan bien que HTTP utiliza estos estandares para el mismo proposito, que es
etiquetar el contenido de manera que el cliente sepa cual es el contenido
Por lo tanto, cuando el cliente solicita una pagina web HTML el servidor puede responder
a la solicitud con algo de HTML etiquetado como text/html
text: es el tipo de medio
HTML es el subtipo

al momento de responder la solicitud el host puede etiquetar el recurso con un tipo de
contenido de imagen / jpeg o / gif o / png para los archivos png
Estos tipos de contenidos son tipos de MIME estandar y son literalmente
lo que aparecera, ese texto aparecera en la respuesta HTTP y la ubicacion donde el cliente puede
analizarlo
Por lo tanto, durante mucho tiempo solia creer que un navegador determinaba el tipo de contenido
que recibia con solo mirar la extencion de el archivo en la URL, pero resulta que no
funciona de esa manera.

De hecho para muchos navegadores, la extension de archivos es el ultimo lugar al que ira el
navegador para determinar el tipo de contenido que esta recibiendo

El primer lugar al que ira (navegador) es el tipo de MIME que devuelve el servidor
si cambiamos la el MIME type (pdf a foo) nos aparece un error que no puedo descargar este archivo
ademas que no se encuentra en MIME map y debes agregarlo
.foo deberia mapear tambien y en este caso podria ser application pdf

el navegador esta confiando en este tipo de conenido para averiguar cual es el contenido
extremos y editemos este tipo MIME y digamos que cuando se sirve un archivo

tiene dos campos:

File name extencion (este no se puede cambiar)
.pdf

MIME type:
application/pdf

CAMBIAMOS

File name extencion (este no se puede cambiar)
.pdf

MIME type:
text/html

digamos que cuando se sirve un archivo PDF, el tipo de MIME debe ser texto/html
que pasa cuando el tipo de MIME cambia

Entonces el navegador se lo dira al navegador que lo que esta recibiendo es HTML, aunque hay
un .pdf en la url
Asi que dejenme hacer

RESULTADO:
el navegador va interpretar el pdf como un texto plano o como un html

Entonces tener tipo MIME incorrectos o daltantes mapeados en la configuracion de
su servidor y esto es cierto para IAS, es cierto para Apache, es cierto para casi
todos los servidores web, pueden causar problemas en su sitio web
Por ejemplo un caso que encontre recientemente fue que los archivos de video
no se publicaron porque los tipos de MIME correctos no estaban

# content negotiation

Aunque tenemos a pensar en HTTP como algo que se utliza para servir paginas web e
imagenes, resulta que la especificacion HTTP describe un protocolo muy generico
para mover informacion de una manera interoparable
Parte del trabajo de mover la informacion es asegurarse de que todos sepan como interpretar la
informacion y es por eso que la ocnfiguracion de tipo de contenido y las asiganaciones MIME son tan
importantes para la web, pero los tipos de medios no son solo para hosts

Los clientes tambien pueden desempenar un papel enel tipo de medio que devuelve un host al
participar en una negociacion de tipo de ocntenido
Un recurso idenficado por una sola URL puede tener multiples representaciones
Tomemos por ejemplo

La receta de brocoli que estabamos viendo antes
Una sola receta puede tener representaciones en diferentes idiomas, como ingles versus frances
vs aleman
tambien podria tener representaciones que difieran en formato HTML vs PDF vs texto plano xml

Es todo el mismo recurso y la misma receta solo representaciones diferentes
La pregunta que no viene a la mente es que representaciones deberia usar el servidor y la respuesta
esta en el mecanismo de negociacion de contenido descrito por la especificacion HTTP

Entonces, cuando un cliente realiza un solicitud HTTP a un servidor

El cliente puede especificar los tipos de medios que aceptaran
Luego los tipos de medios no son solo para que el host los use etiquetar los recursos
salientes, sino que tambien estan siponibles para que los clientes especifiquen los
medios que desean comsumir

El cliente especifica que va a aceptar en el mensaje de solicitud saliente y
de nuevo veremos los detalles de ese mensaje en el siguiente modulo
pero imagine que esta solicitud va al servidor de alimentos (food.com) diciendo que quiero HTML
y oh por la menera tambien quiero esto en frances

Ahora quiero esto en frances. Ahora podria ocurrir que el servidor no tenga HTML para esa receta
disponible. Solo tiene un PDF y lo enviara de vuelta o podria resultar que tiene HTML pero solo una version en ingles
y eso podria decepcionar al usuario, por es por eso qeu lo llamamos negociacion de contenido y no es un ultimatum

De hecho podemos ver la negociacion de contenido en funcionamiento con los idiomas
Por ejm cuando voy a google.com con la configuracion muestra en ingles
Pero cuando vamos a internet opcion y cambiamos el idioma de nuestro navegador
Le estoy anunciando al servidor que prefiero que los recursos esten en frances siempre que sea posible
El servidor lo repetara el idioma del navegador

Por lo tanto los navegadores son piezas de software bastante sofisticadas y pueden manejar muchos tipo de diferentes
de representaciones de recursos
Esta negociacion de contenido es algo que a un usuario probablemente nunca le interesa
salvo para comprar la configuracion de idioma, pero para los desarrolladores de software
usted y yo especialemente las personas que desarrollan negociacion de contenido de servicios web

HTTP es parte de lo que hace que HTTP sea excelente. Un fragmento de codigo escrito
en javascript puede realizar una solicitud al servidor y solicitar una
representacion JSON porque es facil de analizar en el script javascript
Mientras tanto, un fragmento de codigo escrito en C++ puede realizar una solicitud
al mismo servidor en la misma URL y solicitar una representacion XML de un recurso

En ambos casos si el host puede satisfacer esa solicitud, la informacion llega al cliente
en un formato ideal para su analisis

# Where are we?
resorse
URL
representacion

en este modulo web aprendimos que la web y HTTP son todos acerca de los recurso 
Tenemos URL para ubicar esos recursos y tipo de MIME para especificar la 
representacion de esos recursos 
Todo esto fue disenado para hacer las cosas funcionen 
Entonces un servidor Linux puede comunicarse con un cliente de PC y viceversa


