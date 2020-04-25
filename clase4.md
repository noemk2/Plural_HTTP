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

El camnino al recurso

