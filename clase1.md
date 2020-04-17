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
apuntara a un recurso real que se encuentra en el
