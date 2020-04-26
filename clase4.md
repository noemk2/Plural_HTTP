# HTTP architecture

Proxies cahes resources redux

En el 1er hablamos sobre los recursos enfocandonos en las URL
los recursos son la pieza central de HTTP
y ahora que entendemos los mensajes HTTP
Los metodos y las conexiones podemos volver a mirar los recursos bajo una nueva luz

Cual es la esencia de trabajar con los recursos y mensajes

# Resources Redux

Es realmente facil pensar en un recurso web como un archivo en el sistema de archivos del servidor web
Pero
pensar a lo largo de esas lineas realmente no respeta la verdadera capacidad de la abstraccion de recurso

Muchas paginas web requieren recursos fisicos en un sistem de archivos : archivos js, imagens hojas de estilo
sin embargo
los consumidores y usuarios de la web realmente no se perocupan por esos recursos de fondo
en cambio les importan los recursos con los qu pueden interactuar y lo que es mas importante
los recursos que puedan nombrar; por ejm

recursos como la receta beef (filete)
wellington los resultados de busqueda de pizza de plato hondo
el historial medico del paciente 123

Todos estos recurso son los tipos de recursos con los que creamos aplicaciones y el tema comun en la lista
es la importancia de cada uno de estos
elementos sin son lo suficientemente importantes como para que los indetifiquemos y nombremos y
tan
pronto tambien podemos darle al recurso un URL para que alguien localice el recurso
y
una URL es algo util para tener alrededor

por ejm
http://maps.google.com/maps?q=deep+dish+pizza

dada una URL
puedo localizar un recurso por supuesto
pero tambien puedo entregar la URL a otra persona
incrustandola en un hipervinculo
o
enviandola en un correo electronico
Pero hay muchas cosas que no puedo hacer con una URL o mas bien hay mcuhas cosas que una URL no puede hacer

por ejm
una URL no puede restringir el cliente o el servidor a un tipo especifico de tecnologia

Todo el mundo habla HTTP
no importa si su cliente esta en Ruby y su app de servidor esta c++
no importa
ademas que la URL no puede obligar al servidor a almacenar el recurso utilizando ninguna tecnologia en particular
El recurso podria ser un documento en el sistema de archivos pero un marco web tambien podria (frame)
responder a una solicitud entrante para ese recurso y construirlo utilizando informacion almacenada en archivos
almacenada en bases de datos
recuperada de otros servicios web
o simplemente
derivando el recurso desde la hora actual del dia
otra cosa que la url no puede hacer es escpecificar la representacion de un recurso especifico
y
un recurso puede tener multiples representaciones
podria
haber uno en HTML
uno en PDF
uno en ingles
y otro en frances

# Architecural qualities

a parte de pensar en la URL como una apuntador o una unidadadde indreccion entre el cliente y una aplicacion de servidor
Nuevamente la url en si misma no dicta una representacion de recursos especifica
No dicta la implementacion de la tecnologia
No dicta la intencion del cliente en cambio
el cliente expresa la intencion y la representacion deseada en un mensaje HTTP

Un mensaje HTTP es muy simple
Es texto plano como hemos visto
La belleza de eso es como la solicitud y la respuesta

son totalmente audescriptivas
Estan estandarizados

Son faciles de analizar
El mensaje de solicitud incluye el metodo HTTP
que describe lo que el cliente quiere hacer

El camnino al recurso y encabezados adicionales que proporcionan informacion sobre que representacion quiero
la respuesta incluye un codigo de estado para indicar el resultado de una transaccion
encabezados con instrucciones de cache el tipo de contenido del recurso
la longitud del recurso y los metadatos valiosos

debido a que toda la informacion requerida para esta transaccion esta contenida en estos mensajes
y debido a que esa informacion es visible y facil de analizar
las aplicaciones HTTP pueden contar con una cantidad de servicios que brindan

# Adding value

a medida que un mensaje HTTP se mueve del espacio de memoria de un proceso en una maquina
al
espacio de memoria de un proceso en otra maquina
puede moverse a
atraves de
varias piezas de software y hadware que inspeccionan y posiblemente
modifican ese mensaje
un buen ejemplo es
la aplicacion de servidor web en si
un servidor web como IIS o Apache este sera uno de los 1ros destinatarios de un mensaje HTTP entrante
en un maquina servidor y como servidor web es responsable de enrutar los mensajes a la
aplicacion adecuada
Asi que
teniamos
un servidor web que hospedaba 3 sitios diferentes
usando 3 tecnologias distintas
Recibio un mensaje de solicitud HTTP entrante
neceista echar un vistazo dentro de este mensaje
mirar un
encabezado de host
y puede usar eso para descubrir que aplicacion debe recibir y procesar ese mensaje es un escenario
bastante comun y algo muy facil de configurar en IIS y Apache
pero
todos estos servidores web
tambien pueden
realizar acciones adicionales con el mensaje como iniciar sesion en un archivo local
entonces
como el servidor web esta alli y se recibe un mensaje puede tomar
el mensaje y grabarlo en un archivo de registro
tantos detalles como desee
Y del mismo modo
cuando la aplicacion crea el mensaje de respuesta HTTP el servidor tiene oportunidad de
interactuar con ese mensaje a la salida

Essa podria ser una operacion de registro simple pero tambien podria ser una
modificacion directa del mensaje en si

el web server process se puede encarcar de la comprension gzip del recurso de crear log para cada mensaje de http
las applicaiones de servidor no tienen que preocuparse por registrar las transacciones HTTP o agregar comprension
y todo gracias a los mensajes  
autedescriptivos que permiten que las piezas de la infraestructura procesen y transformen estos mensajes HTTP
este tipo de procesamiento tambien puede ocurrir a medida que el mensaje se mueve a traves de

# proxies

estos mensajes HTTP audescriptivos y visibles nos permiten usar servidores proxy
Un servidor proxy es un servidor que se ubica entre un cliente y un servidor  
un proxy es mayormente transparente para el usuario final
entonces
cree que esta enviando una solicitud directamente a un servidor
pero
el mensaje de solicitud HTTP se dirige al proxy que tomara ese mensaje y lo
reenviara al servidor al que desea que llegue
tambien
puede esperar la respuesta del servidor y reenviarla al cliente
pero
antes de reenviar cualquiera de esos mensajes el proxy tambien puede
inspeccionar el mensaje y tomar potencialmente algunas acciones iniciales
por ejemplo
1 de los clientes para los qeu trabajo utiliza un proxy para capturar
todo el trafico HTTP que sale de la oficina

no quieren que los empleados y contratistas pasen su tiempo en Twitter y facebook
por loque las solicitudes HTTP a esos servidores nunca llegaran a sus destinos
y no hay tweet o farmville dentro de la oficina

Ese es un ejm de una funcion popular para un servidor proxy
que es funcionar como un dispositivio de control de acceso
pero
un servidor proxy en realidad puede ser mucho mas sofisticado que simplemente eliminar
mensajes que intenten llegar a hosts especificos
Cualquier firewall podria
hacer eso
Un servidor proxy tambien puede inspeccionar mensajes
eliminar datos confidenciales
como quitar el encabezado del referer de los mensajes HTTP
si ese refere apunta a un recurso interno dentro
de la red de la compania
un proxy de control de acceso tambien puede registrar
todos los mensajes HTTP
crear pistas de auditoria en el trafico
y muchos de estos proxies de control de acceso requieren que
el usuario inicie sesion
antes
de que puede acceder a la web
Ese es un tema que veremos en el quinto modul

El proxy que describo aqui es lo que categorizariamos como un proxy directo un proxy directo suele ser mas cercano al
cliente en la red que a un servidor
generalemnte a uno o 2 saltos de red un cliente en particular
y los proxies hacia adelante generalemnte requieren
alguna configuracion en el sofware del
cliente o en el navegador web para funcionar
la idea es que el proxy directo propocione algunos servicios para
beneficiar solo a los usuarios en una ubicacion particular
no a internet en su conjunto
por lo tanto los usuarios de una empresa especifica o en un edificio de oficinas especifico
o los clientes de un unico proveedor de servicios de internet
otra categoria de servidores proxy es el proxy inverso

# proxy inverso

es un servidor proxy que por lo general esta mas cerca de un servidor que del cliente
y estos son por lo general completamente tansparentes para el cliente
Existe un proxy inverso para proporcionar algun beneficio a un sitio web especifico
y
puede beneficiar indirectamente a todos los usuarios de intenet
ya que todas las solicitudes que lleban a los servidores de ese sitio web provienen del proxy inverso

Ahora ambos tipos de proxies (proxies adelante y proxies inversos pueden proporcionar una amplia gama de servicios)
Por ejemplo
si volvemos al escenario de comprension gzip que hablamos antes un servidor proxy tienen la capacidad de comprimir cuerpos de mensajes
de respuesta
Una empresa puede usar un servidor proxy para la comprension
para quitar parte de la carga del servidor donde realmente vive la aplicacion web
Ahora ni la aplicacion ni el sofware del servidor web en si tienen que preocuparse por la compresion

# proxies services

los proxies tambien puede hacer equilibrio de carga (sistemas monoliticos)
aqui donde un proxies toma los mesajes entrantes y los distribuye a uno de varios servidores web por turnos
o
al saber que servidor esta preocesando
actualmente la menor cantidad de solicitudes
el proxy se asegura de que esas solicitudes se dirijan al servidor correcto
tambien
hay proxies que implementan la aceleracion de SSL
Aqui es donde el servidor proxy realmente realiza el sifrado y descrifrado de los mensajes HTTP
quitando esa carga de los servidores web
Hablare soon

Los proxies tambien pueden agregar una capa adicional de seguridad al filtrar los mensajes HTTP
potencialmente peligrosos especialmente buscar mensajes que puedan tener ataques
de secuencias de comandos entre sitios o ataques de inyeccion SQL incrustados entre ellos

y
finalmente los servidores proxies de almacenamiento en la memoria cache almacena copias de los recursos
a los que se accede con frecuencia y responden a los mensajes que solicitan esos recursos directamente
eso
tipicamente mejora el rendimiento

# caching

El almacenamiento en cache
es una optimizacion para mejorar el rendimiento y la escalabilidad
cuando ha varias solicitudes para la misma representacion de recursos
un servidor puede enviar los bytes a traves de la red una y otra vez
para cada solicitud o un servidor proxy o un cliente puede almacenar en cache la representacion
localmente y reducir la cantidad de tiempo y el ancho de banda necesarios para una
recuperacion completa
El almacenamiento en memoria cache puede ayudar a reducir la latencia ayudar a prevenir los cuellos de botella
y permitir que una aplicacion web sobreviva
cuando cada usuario aparece de inmediato para comprar el producto mas
o ver el ultimo comunicado de prensa
tambien
es un buen ejemplo cuando los metadatos en un mensaje HTTP facilitan capas y servicios adicionales
lo primero que debe saber es que hay 2 tipo de caches
1 cahe publico es un cache compartido entre multiples usuarios generalemnte reside en un servidor proxy
Una memoria cache publica en un proxy directo usualmente almacena en cache los recursos que son populares en
una comunidad de usuarios
como los usuarios
de una compania especifica o los usos de un proveedor de servicios de internet
2 un cache privado esta dedicado a un solo usuario
los navegadores web siempre mantienen un cache privado de recursos en su disco

las reglas sobre que almacenar en el cache , cuando hay que invalidar el cache
con HTTP 1.1 los clientes y los proxies generalmente quieren almacenar en cache una respuesta que tenga un codigo de estado 200
y esa es la respuesta a una solicitud de obtencion HTTP
recuerde
hablamos sobre metodos seguros y no seguros

Cache control
directive | meaning
public | A reponse for everyone
private | A response for a single user
no-cache| Dont cache the response
no-store | You never saw this reponse
