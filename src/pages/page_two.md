---
eleventyNavigation:
  key: operaciones-seguridad

title: Operaciones de Seguridad
ordre: 15
---
Las operaciones de seguridad a menudo están contenidas dentro de un SOC ("Centro de operaciones de seguridad"). Los términos se usan indistintamente.

Por lo general, la responsabilidad del SOC es detectar amenazas en el entorno y evitar que se conviertan en problemas costosos.

## SIEM ("Gestión de eventos de información de seguridad")
La mayoría de los sistemas producen registros que a menudo contienen información de seguridad importante.

Un evento son simplemente observaciones que podemos determinar a partir de registros e información de la red, por ejemplo:

- Usuarios iniciando sesión
- Ataques observados en la red
- Transacciones dentro de las aplicaciones
Un incidente es algo negativo que creemos que afectará a nuestra organización. Podría ser una amenaza definitiva o la posibilidad de que tal amenaza suceda. El SOC debe hacer todo lo posible para determinar qué eventos se pueden concluir como incidentes reales, a los que se debe responder.

El SIEM procesa alertas basadas en registros de diferentes sensores y monitores en la red, cada uno de los cuales puede generar alertas que son importantes para que responda el SOC. El SIEM también puede intentar correlacionar múltiples eventos para determinar alertas.

Los SIEM generalmente permiten analizar eventos de las siguientes áreas:

- La red
- Anfitrión
- Aplicaciones
Los eventos de la red son los más típicos, pero los menos valiosos, ya que no contienen todo el contexto de lo que sucedió. La red generalmente revela quién se comunica dónde, a través de qué protocolos y cuándo, pero no los detalles intrincados sobre qué sucedió, a quién y por qué.

Los eventos del anfitrión brindan más información sobre lo que realmente sucedió y a quién. Desafíos como el cifrado ya no se desdibujan y se gana más visibilidad de lo que está ocurriendo. Muchos SIEM están enriquecidos con grandes detalles sobre lo que sucede en los propios hosts, en lugar de solo en la red.

Los eventos de la aplicación es donde el SOC generalmente puede comprender mejor lo que está sucediendo. Estos eventos brindan información sobre Triple A, AAA ("Autenticación, Autorización y Cuenta"), incluida información detallada sobre cómo se está desempeñando la aplicación y qué están haciendo los usuarios.

Para que un SIEM comprenda los eventos de las aplicaciones, generalmente requiere el trabajo del equipo SOC para que el SIEM comprenda estos eventos, ya que el soporte a menudo no se incluye "listo para usar". Muchas aplicaciones son propiedad de una organización y SIEM aún no comprende los datos que envían las aplicaciones.

## Dotación de personal del SOC
La dotación de personal de un SOC varía mucho según los requisitos y la estructura de una organización. En esta sección, echamos un vistazo rápido a los roles típicos involucrados en la operación de un SOC. Una descripción general de los roles potenciales:

Organización SOC

Como en la mayoría de los equipos organizados, se designa un rol para liderar el departamento. El Jefe del SOC determina la estrategia y las tácticas involucradas para contrarrestar las amenazas contra la organización.

El Arquitecto SOC es responsable de garantizar que los sistemas, las plataformas y la arquitectura general sean capaces de ofrecer lo que los miembros del equipo necesitan para realizar sus funciones. Un SOC Architect ayudará a crear reglas de correlación en múltiples puntos de datos y garantizará que los datos entrantes se ajusten a los requisitos de la plataforma.

El líder del analista es responsable de que se desarrollen y mantengan procesos, o libros de jugadas, para garantizar que los analistas puedan encontrar la información necesaria para concluir alertas e incidentes potenciales.

Los analistas de nivel 1 son los primeros en responder a las alertas. Su deber es, dentro de sus capacidades, concluir alertas y enviar cualquier problema a un analista de nivel superior.

Los Analistas de Nivel 2 se distinguen por tener más experiencia y conocimiento técnico. También deben asegurarse de que cualquier problema en la resolución de alertas se envíe al líder del analista para ayudar a la mejora continua del SOC. El Nivel 2, junto con el Analista Líder, escala los incidentes al Equipo de Respuesta a Incidentes.

El IRT ("Equipo de Respuesta a Incidentes") es una extensión natural del Equipo SOC. El equipo de IRT se despliega para remediar y resolver los problemas que afectan a la organización.

Idealmente, los probadores de penetración también apoyan a la defensa. Los probadores de penetración tienen un conocimiento complejo de cómo operan los atacantes y pueden ayudar en el análisis de la causa raíz y comprender cómo ocurren los robos. La fusión de equipos de ataque y defensa a menudo se conoce como Purple Teaming y se considera una operación de mejores prácticas.

Cadenas de escalada
Algunas alertas requieren acciones inmediatas. Es importante que el SOC haya definido un proceso de a quién contactar cuando ocurren diferentes incidentes. Los incidentes pueden ocurrir en muchas unidades comerciales diferentes, el SOC debe saber a quién contactar, cuándo y en qué medios de comunicación.

Ejemplo de una cadena de escalamiento para incidentes que afectan a una parte de una organización:

Cree un incidente en el sistema de seguimiento de incidentes designado, asignándolo al departamento o a la(s) persona(s) correcta(s)
Si no ocurre ninguna acción directa del departamento/persona(s): envíe SMS y correo electrónico al contacto principal
Si todavía no hay acción directa: llame al contacto principal
Si todavía no hay acción directa: llame al contacto secundario
Clasificación de Incidentes
Los incidentes deben clasificarse según su:

- Categoría
- Criticidad
- Sensibilidad
Según la clasificación de los incidentes y cómo se atribuye, el SOC puede tomar diferentes medidas para resolver el problema en cuestión.

La categoría del incidente determinará cómo responder. Existen muchos tipos de incidentes y es importante que el SOC comprenda lo que significa cada tipo de incidente para la organización. Los incidentes de ejemplo se enumeran a continuación:

- Hackeo interno
- Malware en la estación de trabajo del cliente
- Gusano propagándose por la red
- Ataque de denegación de servicio distribuido
- Credenciales filtradas
La criticidad de un incidente se determina en función de cuántos sistemas se ven afectados, el impacto potencial de no detener el incidente, los sistemas involucrados y muchas otras cosas. Es importante que el SOC pueda determinar con precisión la criticidad para que el incidente pueda cerrarse en consecuencia. La criticidad es lo que determina qué tan rápido se debe responder a un incidente.
¿Se debe responder al incidente de inmediato o el equipo puede esperar hasta mañana?

La sensibilidad determina quién debe ser notificado sobre el incidente. Algunos incidentes requieren extrema discreción.

SOAR ("Orquestación de seguridad, automatización y respuesta")
Para contrarrestar los avances de los actores de amenazas, la automatización es clave para que un SOC moderno responda lo suficientemente rápido. Para facilitar una respuesta rápida a los incidentes, el SOC debe tener herramientas disponibles para orquestar automáticamente soluciones para responder a las amenazas en el entorno.

La estrategia SOAR significa garantizar que el SOC pueda usar datos procesables para ayudar a mitigar y detener las amenazas que se desarrollan más en tiempo real que antes. En entornos tradicionales, los atacantes tardan muy poco tiempo desde el momento del compromiso hasta que se propagan a los sistemas vecinos. Por el contrario, las organizaciones suelen tardar mucho tiempo en detectar las amenazas que han entrado en su entorno. SOAR intenta ayudar a resolver esto.

SOAR incluye conceptos como "Infraestructura como código" de IAC para ayudar a reconstruir y remediar las amenazas. SDN ("Software Defined Networking") para controlar los accesos de forma más fluida y sencilla, y mucho más.

¿Qué monitorear?
Los eventos se pueden recopilar en muchos dispositivos diferentes, pero ¿cómo determinamos qué recopilar y monitorear? Queremos que los troncos tengan la máxima calidad. Registros de alta fidelidad que son relevantes e identificativos para detener rápidamente a los actores de amenazas en nuestras redes. También queremos dificultar que los atacantes eludan las alertas que configuramos.

Si observamos diferentes formas de atrapar a los atacantes, se vuelve evidente dónde debemos enfocarnos. Aquí hay una lista de posibles indicadores que podemos usar para detectar atacantes y qué tan difícil se considera que los atacantes cambien.

Indicator	Difficulty to change
File checksums and hashes	Very Easy
IP Addresses	Easy
Domain Names	Simple
Network and Host Artifacts	Annoying
Tools	Challenging
Tactics, Techniques and Procedures	Hard
Las sumas de verificación y los hashes de archivos se pueden usar para identificar piezas conocidas de malware o herramientas utilizadas por los atacantes. El cambio de estas firmas se considera trivial para los atacantes, ya que su código se puede codificar y cambiar de múltiples maneras diferentes, lo que hace que cambien las sumas de verificación y los hash.

Las direcciones IP también son fáciles de cambiar. Los atacantes pueden usar direcciones IP de otros hosts comprometidos o simplemente usar direcciones IP dentro de la jungla de diferentes proveedores de nube y VPS ("servidor privado virtual").

Los nombres de dominio también pueden ser reconfigurados con bastante facilidad por los atacantes. Un atacante puede configurar un sistema comprometido para usar un DGA ("Algoritmo de generación de dominio") para usar continuamente un nuevo nombre de DNS a medida que pasa el tiempo. Una semana, el sistema comprometido usa un nombre, pero la próxima semana el nombre ha cambiado automáticamente.

Los artefactos de red y host son más molestos de cambiar, ya que esto implica más cambios para los atacantes. Sus utilidades tendrán firmas, como un agente de usuario o la falta de este, que pueden ser recogidos por el SOC.

Las herramientas se vuelven cada vez más difíciles de cambiar para los atacantes. No los hashes de las herramientas, sino cómo se comportan y operan las herramientas al atacar. Las herramientas dejarán rastros en los registros, cargando bibliotecas y otras cosas que podemos monitorear para detectar estas anomalías.

Si los defensores son capaces de identificar las tácticas, las técnicas y los procedimientos que utilizan los atacantes, será aún más difícil para los atacantes llegar a sus objetivos. Por ejemplo, si sabemos que al actor de amenazas le gusta usar Spear-Phishing y luego Pivoting peer-to-peer a través de otros sistemas de víctimas, los defensores pueden usar esto para su beneficio. Los defensores pueden enfocar la capacitación al personal en riesgo de phishing y comenzar a implementar barreras para negar la creación de redes entre pares.