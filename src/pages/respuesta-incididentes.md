---
eleventyNavigation:
  key: incidentes-seguridad

title: Respuesta a Incidentes
ordre: 16
---
# ¿Qué es un incidente?
Un Incidente se puede catalogar como algo adverso, una amenaza, a nuestros sistemas informáticos o redes. Implica daño o alguien que intenta dañar a la organización. No todos los Incidentes serán manejados por un IRT ("Equipo de Respuesta a Incidentes") ya que no necesariamente tienen un impacto, pero los que lo hacen son convocados para ayudar a tratar el incidente de una manera predecible y de alta calidad.

El IRT debe estar estrechamente alineado con los objetivos y metas comerciales de la organización y siempre esforzarse por garantizar el mejor resultado de los incidentes. Por lo general, esto implica reducir las pérdidas monetarias, evitar que los atacantes realicen movimientos laterales y detenerlos antes de que puedan alcanzar sus objetivos.

## IRT - Equipo de respuesta a incidentes
Un IRT es un equipo dedicado a abordar los incidentes de seguridad cibernética. El equipo puede estar formado solo por especialistas en seguridad cibernética, pero puede crear una gran sinergia si también se incluyen recursos de otros grupos. Considere cómo tener las siguientes unidades puede tener un gran impacto en el desempeño de su equipo en ciertas situaciones:

- Especialista en seguridad cibernética: todos sabemos que estos pertenecen al equipo.
- Operaciones de seguridad: pueden tener conocimientos sobre asuntos en desarrollo y pueden brindar apoyo con una vista panorámica de la situación.
- Operaciones de TI
- Operaciones de red
- Desarrollo
- Legal
- HORA
## PICERL - Una Metodología
La Metodología PICERL se llama formalmente NIST-SP 800-61 (https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf) y contiene una descripción general de una metodología que se puede aplicar a incidentes respuesta.

No consideres esta metodología como un modelo en cascada, sino como un proceso en el que puedes avanzar y retroceder. Esto es importante para asegurarse de que se ocupe plenamente de los incidentes que sucedan.

Las 6 etapas de Respuesta a Incidentes:

Preparación
Esta fase es para prepararse para hacer frente a la respuesta a incidentes. Hay muchas cosas que un IRT debe considerar para asegurarse de que estén preparados.

La preparación debe incluir el desarrollo de libros de jugadas y procedimientos que dicten cómo la organización debe responder a ciertos tipos de incidentes. Las reglas de compromiso también deben determinarse de antemano: ¿cómo debe responder el equipo? ¿Debería el equipo tratar activamente de contener y eliminar las amenazas, o a veces es aceptable monitorear una amenaza en el entorno para obtener información valiosa sobre, por ejemplo, cómo irrumpieron, quiénes son y qué buscan?

El equipo también debe asegurarse de tener los registros, la información y el acceso necesarios para llevar a cabo las respuestas. Si el equipo no puede acceder a los sistemas en los que está respondiendo, o si los sistemas no pueden describir con precisión el incidente, el equipo está preparado para fallar.

Las herramientas y la documentación deben estar actualizadas y los canales de comunicación seguros ya se han negociado. El equipo debe asegurarse de que las unidades de negocios y los gerentes necesarios puedan recibir actualizaciones continuas sobre el desarrollo de incidentes que los afecten.

La capacitación tanto para el equipo como para las partes de apoyo de la organización también es esencial para el éxito del equipo. Los respondedores de incidentes pueden buscar capacitación y certificaciones y el equipo puede intentar influir en el resto de la organización para que no se conviertan en víctimas de amenazas.

Identificación
Mirando a través de datos y eventos, tratando de señalar con el dedo algo que debería clasificarse como un incidente. Esta tarea a menudo se encarga al SOC, pero el IRT puede participar en esta actividad y, con su conocimiento, tratar de mejorar la identificación.

Los incidentes a menudo se crean en función de alertas de herramientas relacionadas con la seguridad, como EDR ("Detección y respuesta de punto final"), IDS/IPS ("Sistemas de detección/prevención de intrusiones") o SIEM ("Sistema de gestión de eventos de información de seguridad"). Los incidentes también pueden ocurrir cuando alguien le informa al equipo sobre un problema, por ejemplo, un usuario que llama al equipo, un correo electrónico a la bandeja de entrada de correo electrónico del IRT o un ticket en un sistema de gestión de casos de incidentes.

El objetivo de la fase de identificación es descubrir incidentes y concluir su impacto y alcance. Las preguntas importantes que el equipo debe hacerse incluyen:

¿Cuál es la criticidad y la sensibilidad de la plataforma violada?
¿Se usa la plataforma en otro lugar, lo que significa que existe la posibilidad de un mayor compromiso si no se hace nada a tiempo?
¿Cuántos usuarios y sistemas están involucrados?
¿Qué tipo de credenciales tienen los atacantes y dónde más se pueden reutilizar?
Si es necesario responder a un incidente, el equipo pasa a la siguiente fase de contención.

Contención
La contención debería tratar de detener a los atacantes en seco y evitar daños mayores. Este paso debe garantizar que la organización no sufra más daños y garantizar que los atacantes no puedan alcanzar sus objetivos.

El IRT debe considerar lo antes posible si se debe realizar una copia de seguridad y una imagen. La copia de seguridad y la creación de imágenes son útiles para preservar la evidencia para más adelante. Este proceso debe tratar de asegurar:

Una copia de los discos duros involucrados para el análisis forense de archivos.
Una copia de la memoria de los sistemas involucrados para análisis forense de memoria.
Hay muchas acciones que el IRT puede realizar para detener a los atacantes, lo que depende en gran medida del incidente en cuestión:

Bloqueando a los atacantes en el Firewall
Desconexión de la conectividad de red a los sistemas comprometidos
Poner sistemas fuera de línea
Cambio de contraseñas
Solicitar ayuda al ISP ("Proveedor de servicios de Internet") u otros socios para detener a los atacantes
Las acciones realizadas en la fase de contención intentan eliminar rápidamente al atacante para que el IRT pueda pasar a la fase de erradicación.

Erradicación
Si la contención se ha realizado correctamente, el IRT puede pasar a la fase de erradicación, a veces llamada fase de remediación. En esta fase, el objetivo es eliminar los artefactos de los atacantes.

Existen opciones rápidas para asegurar la erradicación, por ejemplo:

Restaurar desde una buena copia de seguridad conocida
Reconstruyendo el servicio
Si se han implementado cambios y configuraciones como parte de la contención, tenga en cuenta que restaurar o reconstruir puede deshacer estos cambios y tendría que volver a aplicarlos. A veces, sin embargo, IRT debe intentar eliminar manualmente los artefactos dejados por un atacante.

Recuperación
Restaurar las operaciones normales es el estado objetivo para el IRT. Esto podría implicar pruebas de aceptación de las unidades de negocio. Idealmente agregamos soluciones de monitoreo con información sobre el incidente. Queremos descubrir si los atacantes regresan repentinamente, por ejemplo, debido a artefactos que no pudimos eliminar durante la erradicación.

Lecciones aprendidas
La fase final implica que tomemos lecciones del incidente. Es probable que haya muchas lecciones del incidente, por ejemplo:

¿El IRT tenía los conocimientos, herramientas y accesos necesarios para realizar su trabajo con alta eficiencia?
¿Faltó algún registro que podría haber hecho que los esfuerzos de IRT fueran más fáciles y rápidos?
¿Hay algún proceso que podría mejorarse para evitar que ocurran incidentes similares en el futuro?
La fase de lecciones aprendidas generalmente concluye con un informe que detalla un resumen ejecutivo y una descripción general de todo lo que sucedió durante el incidente.