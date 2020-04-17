HTTP es el protocolo que me permite buscar 'hornos de microhornas'
y comprar uno en amazon
Tambien es el protocolo que me permite reunirme con viejos amigos en un chat de facebook
o cuando no hay nada bueno en la television, puedo ir a youtube
y ver videos de gatos haciendo cosas graciosas

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
HTML es una pagina, vera etiquetas, script, etiquetas de imagenes y etiquetas images, etiquetas de estilo que apuntara a URL adicionales
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

