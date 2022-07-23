---
eleventyNavigation:
  key: comunicacion-entre-redes

title: Comunicación entre redes
ordre: 5
---
## Protocolos y Redes
Es esencial que los profesionales de la seguridad cibernética tengan una comprensión sólida de cómo se comunican las computadoras. Hay muchas más cosas detrás de escena de las redes informáticas que las que se pueden observar cuando se usan aplicaciones.

## El modelo OSI
El modelo OSI ("Interconexión de sistemas abiertos") representa una forma fácil e intuitiva de estandarizar las diferentes partes necesarias para comunicarse a través de redes.

El modelo aclara lo que se requiere para comunicarse en una red al dividir los requisitos en varias capas.

Así es como se ve el modelo OSI:


7.  Solicitud	Donde los humanos procesan datos e información
6. Presentación	Garantiza que los datos estén en un formato utilizable
5. Sesión	Capaz de mantener conexiones
4. Transporte	Los datos se reenvían a un servicio capaz de manejar solicitudes
3. Capa de red	Responsable de qué ruta deben viajar los paquetes en una red
2. Enlace de datos	Responsable de a qué dispositivos físicos deben ir los paquetes
1. Físico	La infraestructura física para transportar datos

Las 3 capas superiores generalmente se implementan en software dentro del sistema operativo:


7. Solicitud	Software
6. Presentación	Software
5. Sesión	Software

Las 3 capas inferiores normalmente se implementan en el hardware dentro de los dispositivos de la red, por ejemplo, conmutadores, enrutadores y cortafuegos:


3. Capa de red	Hardware
2.  Enlace de datos	Hardware
1.  Físico	Hardware

La capa 4, la capa de transporte, conecta el software con las capas de hardware.

SDN ("Software Defined Networking") es una tecnología que permite implementar más capas del hardware a través del software.



## Capa 7 - Capa de aplicación
La lógica del negocio y la funcionalidad de la aplicación se encuentran aquí. Esto es lo que usan los usuarios para interactuar con los servicios a través de una red. La mayoría de los desarrolladores crean aplicaciones en la capa de aplicación.

La mayoría de las aplicaciones que usa están en la capa de aplicación, con la complejidad de las otras capas ocultas.

Ejemplos de aplicaciones de capa 7:

- HTTP ("Protocolo de transferencia de hipertexto"): nos permite acceder a aplicaciones web
- FTP ("Protocolo de transferencia de archivos"): permite a los usuarios transferir archivos
- SNMP ("Protocolo simple de administración de red"): protocolo para leer y actualizar configuraciones de dispositivos de red

Hay muchas aplicaciones que usan estos protocolos como Google Chrome, Microsoft Skype y FileZilla.

> ¡Está accediendo a esta clase a través de la Capa 7!

## Capa 6 - Capa de presentación
Normalmente es una capa invisible, pero es responsable de adaptar, transformar y traducir datos. Esto es para garantizar que la aplicación y las capas inferiores puedan entenderse entre sí.

- Esquemas de codificación utilizados para representar texto y datos, por ejemplo, ASCII (Código estándar estadounidense para el intercambio de información) y UTF (Formato de transformación Unicode).
- Cifrado para servicios, por ejemplo SSL ("Secure Sockets Layer") y TLS ("Transport Security Layer")
- Compresión, por ejemplo, GZip en uso en muchas implementaciones de HTTP.
## Capa 5 - Capa de sesión
 La responsabilidad de esta capa es manejar las conexiones entre la aplicación y las capas inferiores. Implica establecer, mantener y finalizar conexiones, también denominadas sesiones.

Los protocolos comunes que representan bien la capa de sesión son:

- SOCKS: un protocolo para enviar paquetes a través de un servidor proxy.
- NetBIOS: un protocolo antiguo de Windows para establecer sesiones y resolver nombres.
- SIP ("Protocolo de inicio de sesión"): para participar en comunicaciones VOIP ("Voice Over IP")
## Capa 4 - Transporte
La capa que permite representar las aplicaciones en la red.

Algunas aplicaciones bien conocidas en esta capa:

- TCP ("Protocolo de control de transmisión"): se utiliza para muchas aplicaciones, lo que garantiza la estabilidad, el control de la cantidad de datos que se pueden enviar en un momento dado, la confiabilidad y más.
- UDP ("Protocolo de datagramas de usuario"): uso de protocolo ligero y rápido para muchos servicios.
- QUIC ("Conexiones de Internet UDP rápidas"): un protocolo diseñado para conexiones más rápidas y va de la mano con la versión 2 del protocolo HTTP.
## Capa 3 - Red
Una capa responsable de enrutar paquetes entre redes a través de enrutadores.

En esta capa residen los siguientes protocolos:

- IP ("Protocolo de Internet"): se utiliza todos los días al acceder a Internet. Viene en dos versiones, IP versión 4 y 6.
- ICMP ("Protocolo de mensajes de control de Internet"): utilizado por dispositivos de red y operadores de red, para diagnosticar conexiones de red o para que los dispositivos envíen y respondan a condiciones de error y más.
- IPSec ("Protocolo de seguridad de Internet"): permite conexiones cifradas y seguras entre dos dispositivos de red.
## Capa 2 - Enlace
Las redes de enlace, como su nombre lo indica, consisten en protocolos diseñados para enviar paquetes a través de los enlaces reales (conexiones físicas) a los que están conectados los nodos de la red. Una forma más sencilla de pensarlo es que la capa de enlace es responsable de mover los datos de lo físico a lo lógico (a la capa de red).

Los protocolos en esta capa incluyen:

- Ethernet: un protocolo esencial utilizado por la mayoría de los sistemas operativos cuando se conectan a redes mediante un cable físico.
- Wi-Fi ("Fidelidad inalámbrica"): para acceder a redes a través de señales de radio. Utiliza una familia de protocolos llamada IEEE 802.11.xx
NDP ("Protocolo de descubrimiento de vecinos"): IP versión 6 (IPv6) utiliza este protocolo en la capa de enlace para recopilar la información necesaria para comunicarse a través de IPv6
## Capa 1 - Física
La capa física representa la señalización que permite la transferencia de bits y bytes entre un medio físico. Puede transmitirse por radio o señales a través de un cable, utilizando señales eléctricas o luz, por ejemplo, fibra.

Los ejemplos de los protocolos de capa física incluyen:

- Bus CAN ("Red de área del controlador"): se utiliza en microcontroladores y otros dispositivos para comunicarse con otros dispositivos similares, sin involucrar una computadora. A menudo se usa en ICS ("Sistemas de control industrial").
- Capa física de Ethernet: utilizada por Ethernet en la capa física para enviar señales con velocidades de hasta muchos gigabits de tráfico por segundo.
- Capa física de Bluetooth: Bluetooth también tiene sus propias especificaciones sobre cómo se deben enviar y recibir las señales de radio.