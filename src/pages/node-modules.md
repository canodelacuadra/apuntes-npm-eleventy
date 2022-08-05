---
eleventyNavigation:
  key: node-modules
  parent: npm
title: Node Modules

ordre: 10
---
La carpeta node_modules es un directorio que se crea en la carpeta raíz de nuestro proyecto cuando instalamos paquetes o dependencias mediante npm. De esta forma, desde nuestro código Javascript podemos importar paquetes externos instalados mediante npm, teniéndolos en nuestro proyecto local (no dependen de una ruta externa al proyecto) y sin necesidad de manipularlos manualmente.

Para cargar dichas librerías o paquetes en nuestro código Javascript, utilizaríamos algo así:
````js
import { Howler, Howl } from "howler";
import { data } from "./data/Information.js";
````
Observa que en el segundo caso, importamos desde una ruta con un fichero Javascript, pero en el primer caso, no se trata de una ruta, sino de una palabra clave. Esa palabra clave es el nombre de la carpeta en node_modules de la librería que vamos a utilizar, y este tipo de importación es lo que se llama un **bare import** o modulos desnudos que la permiten ciertos entornos como nodejs.


## ¿Qué es node_modules? 
Básicamente, cualquier paquete instalado, se almacena dentro de la carpeta node_modules del proyecto, en una carpeta con el nombre del paquete, junto a todos sus ficheros necesarios y dependencias respectivas .

Es por esto, que es bueno tener en cuenta una serie de detalles relacionados con esta carpeta, el espacio que ocupa y como administrarlo.

## Dependencias instaladas 
Para saber que dependencias tengo instaladas en un proyecto basta con hacer utilizar el comando npm list, aunque generalmente lo acompañaremos del parámetro ``--depth 0`` para que no nos muestre todo el árbol completo de dependencias, sino solo los paquetes directos del proyecto principal:

````bash
$ npm list --depth 0
frontend-project@1.0.0 /home/manz/github/frontend-project
├── howler@2.2.0
├── lit-element@2.0.1
└── react@16.13.1
````
En este caso, vemos que en el proyecto estamos usando las dependencias howler, lit-element y react, con sus respectivas versiones. Sin embargo, podemos ir aumentando el número del parámetro depth, para que nos muestre las dependencias que usa cada dependencia del proyecto:
````
$ npm list --depth 1
frontend-project@1.0.0 /home/manz/github/frontend-project
├── howler@2.2.0
├─┬ lit-element@2.0.1
│ └── lit-html@1.2.1
└─┬ react@16.13.1
  ├── loose-envify@1.4.0
  ├── object-assign@4.1.1
  └── prop-types@15.7.2
````
Por ejemplo, vemos que howler no tiene dependencias, mientras que lit-element tiene lit-html como única dependencia y react usa las dependencias loose-envify, object-assing y prop-types.

Si ampliamos el parámetro depth a 3, podremos ver las dependencias que tienen las dependencias de las dependencias del proyecto (parece un trabalenguas):
````bash
$ npm list --depth 2

frontend-project@1.0.0 /home/manz/github/frontend-project
├── howler@2.2.0
├─┬ lit-element@2.0.1
│ └── lit-html@1.2.1
└─┬ react@16.13.1
  ├─┬ loose-envify@1.4.0
  │ └── js-tokens@4.0.0
  ├── object-assign@4.1.1
  └─┬ prop-types@15.7.2
    ├── loose-envify@1.4.0 deduped
    ├── object-assign@4.1.1 deduped
    └── react-is@16.13.1
````
Vemos que la dependencia loose-envify de React, usa la dependencia js-tokens, mientras que prop-types usa losee-envify, object-assign y react-is. Observa la palabra clave deduped que aparece al lado de algunas dependencias, puesto que volveremos a ella a continuación.


## Unificar dependencias 
Si observaste bien el último ejemplo anterior, te habrás dado cuenta que las dependencias loose-envify y object-assign se repiten, son dependencias tanto de react como de prop-types, por lo que estarían repetidas. Para evitar desperdiciar espacio y tener paquetes redundantes de este tipo, npm realiza una tarea que denomina deduplicar paquetes.

Generalmente, estas tareas se hacen automáticamente al instalar paquetes, pero puedes forzar a npm a revisar todas las dependencias del proyecto y unificar dependencias escribiendo el siguiente comando:
````
$ npm dedupe
````
De esta forma obligamos a revisar los paquetes y unificar dependencias si es posible.

### Calcular tamaño de paquetes 
Aunque podríamos utilizar comandos como du o ncdu para calcular el espacio utilizado en la carpeta node_modules, existen algunas herramientas que nos harán el trabajo más sencillo y cómodo.

Ten en cuenta que cada una de estas herramientas tiene sus propias formas de calcular los datos, e incluso calculan diferentes detalles (teniendo en cuenta diferentes variables y factores), por lo que hay que asegurarse de que los datos son realmente lo que buscamos (tamaño de descarga, tamaño de instalación, tamaño final al crear un bundle, etc...).

Las herramientas más conocidas son las siguientes:

* npm-size	Muestra el tamaño total de las dependencias indicadas después de hacer un npm install.
* package-size	Muestra el tamaño final de un bundle que utilice la lista de dependencias indicadas.
* download-size	Calcula el tamaño total sin hacer un npm install. Usa npm-download-size.
* howfat	Comprueba el tamaño total y número de dependencias del proyecto.
* cost-of-modules	Comprueba el tamaño de todos los paquetes que usas en tu proyecto.
* bundlephobia.com	Online. Muestra el tamaño que ocuparía el paquete al hacer un bundle (bundle size).
* packagephobia.com	Online. Muestra el tamaño del paquete (publish size) y el de un npm install (install size).

Observa que en los siguientes ejemplos, realizamos varios comandos encadenados que nos devuelven las dependencias de nuestro proyecto. Finalmente, con xargs unimos los resultados en una sola linea, creando una lista con todas las dependencias separadas por espacios.

En el primer caso, las ejecutamos con npm-size:
````
$ npx npm-size howler lit-element react
  ✔ howler@2.2.0      368 KB
  ✔ lit-element@2.3.1 1.6 MB
  ✔ react@16.13.1     408.91 KB
````
En el segundo caso, las ejecutamos con package-size, el cuál nos diferencia entre el tamaño de la librería, y sus tamaños minificados o incluso comprimidos con gzip, como muchos servidores web lo hacen de forma transparente:
````
$ npx package-size howler lit-element react

  package            size       minified  gzipped
  howler@2.2.0       106.09 KB  35.32 KB  9.26 KB
  lit-element@2.3.1  151.65 KB  22.59 KB  6.96 KB
  react@16.13.1      68.82 KB   7.41 KB   2.77 KB
````
En el caso de download-size, lo que se evalua es el tamaño de descarga de cada paquete, antes de realizar el npm install. Obtiene los datos de una API de la web de npm-download-size:
````
$ npx download-size howler lit-element react
howler@2.2.0: 80.35 KiB
lit-element@2.3.1: 216.60 KiB
react@16.13.1: 93.23 KiB
````
En el último caso, donde utilizamos howfat, no nos devuelve los valores por separado, sino que nos da los datos totales de la suma de las dependencias indicadas:
````
$ npx howfat howler lit-element react
Dependencies: 6
Size: 1.92mb
Files: 590
````
En los ejemplos anteriores, en lugar de escribir los paquetes manualmente, podemos ejecutar la siguiente linea de comandos, que obtendrá la lista de paquetes del package.json y ejecutará la herramienta especificada al final pasándolos por parámetro:
````bash
$ cat package.json | jq .dependencies | jq -r 'keys[]' | xargs npx npm-size
````
La utilidad cost-of-modules probablemente sea la más simple, ya que con un npx cost-of-modules se encargará de calcular el tamaño de cada dependencia y mostrarlo en una tabla, junto al número de dependencias. También puedes utilizar bundle-phobia-cli, una versión de línea de comandos que usa BundlePhobia.

## Liberar espacio en node_modules 
Como hemos comentado hasta ahora, si tenemos varios proyectos en nuestro disco duro, es muy habitual tener carpetas node_modules en el disco, ocupando megas o incluso gigas de datos.

Existe una herramienta muy interesante llamada npkill para buscar, revisar cuanto ocupan y eliminar carpetas node_modules por nuestro disco duro. Nos mostrará una sencilla interfaz por donde nos podemos ir desplazando y marcando con SPACE las carpetas que queramos eliminar:
````
npkill: eliminando node_modules
````
NPM también incorpora un comando denominado npm prune, que revisa la carpeta node_modules en busca de paquetes que ya no se utilicen o que por error se han quedado huérfanos en dicha carpeta (problemas, instalaciones de npm no terminadas, etc...) e intenta optimizarlas y reducir su tamaño.

## ¿Quién usa esta dependencia? 
Es muy posible que en proyectos grandes donde se utilizan muchos paquetes, quieras buscar que paquete está usando una dependencia concreta. Vamos a hacer un ejemplo con la dependencia loose-envify, que sabemos que la utiliza react y una de sus dependencias:
````
$ npm list loose-envify
frontend-project@1.0.0 /home/manz/github/frontend-project
└─┬ react@16.13.1
  ├── loose-envify@1.4.0
  └─┬ prop-types@15.7.2
    └── loose-envify@1.4.0  deduped
````
En nuestra terminal, npm resaltará en amarillo los paquetes coincidentes con la dependencia que hemos especificado por parámetro, pudiendo incluso indicar varias dependencias en varios parámetros.

Existe también una utilidad llamada npm-why que permite realizar esta misma tarea, mostrándolo de forma más visual, mediante unas «migas de pan» para no perdernos:
````
$ npx npm-why loose-envify

  Who required loose-envify:

  frontend-project > react > loose-envify@1.4.0
  frontend-project > react > prop-types > loose-envify@1.4.0
````
## Vulnerabilidades (seguridad) 
En algunas ocasiones, podemos encontrarnos con problemas de seguridad en nuestros proyectos. Esto frecuentemente ocurre porque a una de las dependencias que utilizamos (o a una de sus respectivas dependencias) se le ha descubierto un problema de seguridad. NPM tiene un sistema que revisa las dependencias instaladas y te notifica si encuentra alguna versión vulnerable:
````
$ npm install

audited 7 packages in 0.552s
found 2 vulnerabilities (1 moderate, 1 high)
  run `npm audit fix` to fix them, or `npm audit` for details
````
En el caso de encontrarnos en esta situación y nuestro proyecto se encuentre con un problema de seguridad, conviene revisar los paquetes o dependencias implicados y decidir que medida tomar. Dichas vulnerabilidades se suelen dividir en varios niveles: low (nivel bajo), moderate (nivel medio) y high (nivel peligroso).

Ejecutando el comando npm audit, nos mostrará varias tablas de resumen con información sobre el problema de seguridad:

## Vulnerabilidades: npm audit fix

Una vez detectados los paquetes con la vulnerabilidad (podemos utilizar el método del apartado anterior para localizar el paquete que utiliza la dependencia vulnerable), podemos intentar realizar una de las siguientes acciones:

* Intentar resolverlo automáticamente con el comando npm audit fix.
* Si no es posible, revisar actualizaciones del paquete vulnerable y hacerlo manualmente.
* Si no es posible, revisar issues del paquete vulnerable. Normalmente se trata el problema.
Si ninguna de estas opciones nos sirve, quizás, la mejor forma sería estudiar si hay algún paquete alternativo que podamos reemplazar y adaptar por el vulnerable. Mencionar también que los casos más graves de vulnerabilidades se dan cuando el paquete vulnerable es un paquete de producción, es decir, va a estar presente en la web definitiva, expuesto a usuarios.