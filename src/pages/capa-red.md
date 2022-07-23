---
eleventyNavigation:
  key: capa-red

title: Capa de Red en Profundidad
ordre: 6
---
## IP - El Protocolo de Internet
IP se utiliza para comunicarse a través de redes, no solo a través de enlaces físicos, sino también entre redes de enrutadores. El esquema de direccionamiento en uso es IPv4 ("IP Versión 4") o IPv6 ("IP Versión 6").

Las redes IP se pueden dividir en diferentes secciones, a menudo denominadas subredes. Esto se logra agregando una pieza adicional de información, junto con la dirección IP, llamada máscara de red . La máscara de red dicta qué tan grande es una red y qué paquete se enruta dentro de la red y cuál debe enrutarse fuera de la red.

Las máscaras de red se pueden representar a través de números decimales o con una notación de barra oblicua. Cuando se usa la notación de barra inclinada, la barra inclinada sigue la dirección IP del sistema. Aquí hay unos ejemplos:

|IP Address|	Slash Notation|	Netmask|
|--|--|--|
|10.0.0.1|	/8   - Example: 10.0.0.1/8	|255.0.0.0|
|172.16.1.1|	/12 - Example: 172.16.1.1/12|	255.240.0.0|
|192.168.0.1|	/16 - Example: 192.168.0.1/16|	255.255.0.0|
|192.168.0.1|	/24 - Example: 192.168.0.1/24|	255.255.255.0|

Algunas redes IP están reservadas solo para cierto tipo de tráfico. Las direcciones IP de la tabla anterior están reservadas solo para uso organizacional interno, lo que significa que no deben enrutarse en Internet. Este tipo de direcciones IP se conocen comúnmente como direcciones RFC1918.

## Redes diferentes
Echemos un vistazo a las diferentes redes dentro de RFC1918 y qué tan grandes son las redes:

- 10.0.0.0/8 - Más de 16 millones de direcciones IP
- 172.16.0.0/12: alrededor de 1 millón de direcciones IP
- 92.168.0.0/16 - 65534 direcciones IP
Los segmentos de IP se pueden dividir aún más en redes más pequeñas y granulares.

Cada red tiene una dirección reservada para transmitir el tráfico a cada host de la red, esto se denomina dirección de transmisión. La transmisión de datos significa enviar datos a todos en la red en lugar de enviarlos a un solo host. Hay muchas aplicaciones y protocolos que se basan en el tráfico de difusión para que funcionen.

Para cada segmento de red, la transmisión es siempre la última dirección IP de la red. Por ejemplo, en la red 192.168.0.0/24, la dirección de transmisión es 192.168.0.255.

La máscara de red más pequeña posible es 255.255.255.255, representada como /32. Esta red solo tiene una dirección IP.

Si es necesario enviar tráfico de regreso al host, por ejemplo, para comunicaciones entre aplicaciones, se envía a la dirección del host local. Esta dirección es siempre 127.0.0.1 y es una red /8.

En las redes IP el tráfico es enrutado por un enrutador. Un enrutador es un dispositivo de red que comprende el formato IP y puede reenviar paquetes entre redes. Esto es diferente a un conmutador, ya que el conmutador reenvía datos dentro de una red, mientras que el enrutador reenvía entre redes.


Puede verificar su dirección IP en Windows ejecutando el comando ipconfig dentro de una ventana de línea de comandos. En Linux esto se hace con el comando ip addr show o .ifconfig

Cuando una computadora necesita comunicarse con algo que no se puede encontrar en la LAN, envía tráfico a la puerta de enlace predeterminada según cómo esté configurado el sistema. La puerta de enlace predeterminada es un enrutador que es capaz de reenviar el tráfico a la dirección IP de destino.


## NAT ("Traducción de direcciones de red")
NAT permite que un sistema que acepta conexiones en una dirección IP pública asigne esas solicitudes a una dirección IP RFC 1918 interna o viceversa. Los sistemas que realizan NAT suelen ser cortafuegos y enrutadores.

Una implementación típica de NAT es donde la dirección IP externa se usa como fachada para varias direcciones IP internas, y el número de puerto de destino se usa para decidir a qué servidor se deben enviar los datos. Esto permite que las direcciones IP internas reciban tráfico de sistemas externos.

Puerto NAT

Otra implementación muy común es permitir que las direcciones IP internas accedan a Internet con una dirección IP externa. El NAT realiza un seguimiento de las conexiones desde las direcciones internas a las de destino y reenvía el tráfico a través de las conexiones.

NAT se puede configurar de muchas maneras, pero en esta clase no entraremos en más detalles del método.

Nota : NAT permite que los ingenieros de red sean más flexibles con sus implementaciones, lo que permite que se desarrollen muchos casos de uso diferentes.
IPv6 - IP Versión 6
La versión 6 de IP es el estándar más reciente para IP y se creó para admitir más direcciones IP. En lugar de utilizar 32 bits de direccionamiento para direcciones IP, se utilizan 128 bits. Esto permite suficientes direcciones IP para el futuro previsible, mientras que IPv4 ya se ha agotado.

Las direcciones IPv6 utilizan 8 grupos de 4 números hexadecimales. Una dirección IPv6 se ve así: 2a00:1450:400f:80a::200e:. Note que no tiene los 8 grupos de 4 números hexadecimales. Esto se debe a que las direcciones IPv6 se pueden acortar mediante reglas simples:

Los 0 iniciales se pueden acortar
Los dos puntos dobles (::) se pueden usar para representar una cadena continua de ceros.
La dirección IPv6 expandida es: 2a00:1450:400f:080a:0000:0000:0000:200e.

El host local se puede reducir a ::1 y ::.

IPv6 tiene redes, es decir, subredes, al igual que IPv4.

El encabezado de IPv6 se ve así:

Encabezado IPv6

Podemos ver un encabezado mucho más simple con mucho más espacio para el direccionamiento IP.

IPv6 se usa cada vez más, y hay soporte integrado para este protocolo en muchas herramientas. Por ejemplo ping, podemos cambiar entre IPv4 e IPv6 con el indicador -4 y -6 respectivamente.

Ejecute ipconfigy vea si ve alguna dirección IPv6. Si tiene habilitado IPv6, intente ping -6 google.comy ping -4 google.com. ¿Ves cómo el comando nos permite usar IPv4 o IPv6?

Nota: si no tiene IPv6 hoy, hay muchos servicios de nube pública que le otorgarán una dirección IPv6 pública hoy que puede usar para experimentar y explorar.
ICMP
ICMP a menudo se asocia con Ping y Traceroute. ICMP se puede usar para otras cosas, como pedirle a un nodo su hora, lo que se conoce como una solicitud de marca de tiempo ICMP. Una solicitud de marca de tiempo ICMP simplemente permite, por ejemplo, que un enrutador solicite a otro enrutador que sincronice su hora, un atributo importante en las comunicaciones de red.

Una táctica común para que los atacantes verifiquen si los sistemas están disponibles en una red es realizar un barrido de ping. El objetivo de dicha actividad es hacer que el dispositivo de destino en un rango de red responda a las solicitudes de ping para que el atacante sepa que está disponible. Este enfoque es ingenuo ya que muchos sistemas bloquean por defecto los pings entrantes.

trazarruta
Tracerouting es una forma de determinar qué enrutadores están involucrados en el envío de un paquete del sistema A al B. Saber qué enrutadores toman nuestros paquetes puede ser útil tanto para comprender mejor nuestras redes como para comprender la superficie de ataque. Un enrutador es responsable de enrutar el paquete en la dirección correcta. Imagínese esto como si estuviera conduciendo por una carretera, donde las señales de tráfico en las intersecciones le guían hasta su destino. Estos letreros en las intersecciones representan enrutadores. Traceroute identifica estas señales e intersecciones y te dice qué tan lejos están, medido en milisegundos (ms).

Los encabezados IPv4 TTL e IPv6 Hop Limit tienen la misma función. Cada enrutador que enruta un paquete disminuirá este valor en 1, y si el valor llega a 0, el enrutador descartará el paquete y devolverá un paquete ICMP con tiempo excedido al remitente.

Para realizar un rastreo de ruta en Windows:

tracert google.com
Para realizar un traceroute en Linux (no instalado por defecto):

traceroute google.com
El proceso de rastreo de ruta a través de estas herramientas es simple:

El sistema operativo envía un paquete google.com, el valor TTL se establece en 1.
El paquete se enruta en la red y el primer enrutador disminuye el TTL en 1, dejándolo en 0. Esto hace que el enrutador descarte el paquete y envíe "ICMP Time Exceeded" de regreso a la fuente.
El cliente aumenta el TTL 1, lo que permite enrutar el paquete a través de un salto adicional.
Este proceso se repite aumentando el TTL en 1 hasta llegar al destino.

DNS ("Sistema de nombres de dominio")
El DNS se utiliza para asignar aplicaciones, a través de nombres, a direcciones IP. Por ejemplo, si desea usar su navegador para visitar http://google.com, el navegador primero debe realizar una solicitud a un servidor DNS para resolver la dirección IP detrás de google.com.

Los sistemas normalmente se configuran con un servidor de nombres de dominio primario y secundario. Estos ajustes pueden configurarse manualmente o ser proporcionados por un servidor DHCP. Esto permite que nuestros sistemas informáticos lleguen a un servidor DNS para que lo resuelva por nosotros.

El servidor DNS es entonces responsable de resolver la solicitud. Luego procederá a verificar su propio caché para ver si ya conoce la respuesta. Cada respuesta de DNS se puede almacenar en caché, es decir, se almacena temporalmente para acelerar futuras solicitudes, durante un cierto TTL ("Tiempo de vida"). El TTL normalmente se establece en un par de minutos, por ejemplo, 10 minutos.

Si un servidor DNS no tiene una respuesta en su caché, procederá a verificar quién es el responsable de dar la respuesta. Esto se realiza a través de un proceso recursivo que implica solicitar un sistema jerárquico de servidores de nombres que inevitablemente hará que la solicitud de DNS termine en el servidor de nombres autorizado.

Puede intentar hacer una búsqueda de DNS con Windows o Linux ahora. Desde una terminal de línea de comandos en tipo Windows nslookup w3schools.com, o en tipo Linux dig w3schools.com. Debería ver una salida como esta:

excavación de DNS

La dirección IP de w3schools.com se puede ver en el ;; SECCIÓN DE RESPUESTAS. Cuando se capturó esta captura de pantalla, la dirección IP detrás del nombre w3schools.com era 66.29.212.110 .

El Servidor de nombres autorizados es el servidor DNS que se encarga de dar la respuesta definitiva a una pregunta. Por ejemplo, la dirección IP de google.com será respondida por su servidor de nombres autorizado, y podemos ver este servidor al consultarlo:

Encontrar un servidor de nombres autorizado en Windows:

nslookup -type=SOA google.com
Encontrar un servidor de nombres autorizado en Linux:

dig -t SOA google.com
DHCP ("Protocolo de configuración de host dinámico")
Como su nombre lo indica, el protocolo DHCP permite que cualquier sistema en una red se comunique con un servidor y reciba una configuración. Dicha configuración generalmente implica recibir la dirección IP y el rango de red, la puerta de enlace predeterminada y los servidores DNS.

DHCP permite una fácil gestión de los clientes que se unen y abandonan una red.

Si tiene curiosidad si está utilizando DHCP en este momento, puede escribir ipconfig /allen un sistema Windows y buscar "DHCP habilitado: sí" en la salida. Su computadora puede tener múltiples interfaces de red

VPN ("Red Privada Virtual")
Una VPN es un sistema que permite que dos sistemas establezcan formas encriptadas para la comunicación, lo que permite encriptar el tráfico de la red en tránsito. Muchas VPN son una arquitectura de cliente a servidor, lo que permite al cliente acceder a múltiples servicios detrás de la VPN. También es probable que las VPN alojadas en su lugar de trabajo brinden acceso a recursos que, de otro modo, solo serían accesibles desde el interior.

vpn

Algunos servicios VPN están diseñados para la privacidad del usuario y el cifrado de datos en tránsito. Estos servicios permiten a los usuarios enviar datos de red a través de la VPN, enmascarando efectivamente la dirección IP de los usuarios cuando navegan por Internet.

En general, es una buena práctica usar VPN para proteger las comunicaciones de su red; sin embargo, no debemos usar ningún tipo de servicio de VPN. Los servicios VPN gratuitos a veces pueden ser maliciosos, ya que inspeccionan, leen y almacenan sus datos confidenciales.

VPN maliciosa