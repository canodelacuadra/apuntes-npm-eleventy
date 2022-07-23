---
eleventyNavigation:
  key: instalar-desinstalar-npm
  parent: npm
title: Instalar y desinstalar paquetes con npm

ordre: 3
---
La finalidad de npm es instalar desinstalar y mantener) los paquetes (dependencias) de un proyecto de forma cómoda, rápida y amigable para el desarrollador, permitiendo ahorrar tiempo y esfuerzo.

Para ello, utilizaremos principalmente el comando install y uninstall de npm, además de un pequeño ayudante denominado npx, que explicaremos a continuación:


* npm install ``<paquete>``	Instala el paquete indicado en node_modules/, asociándolo al proyecto.
* npm uninstall ``<paquete>``	Desinstala el paquete indicado, eliminándolo de node_modules/.
* npx ``<comando>``	Ejecuta paquetes CLI instalados a nivel de proyecto (o no instalados).
Es posible abreviar o utilizar alias en ciertos comandos. Por ejemplo npm add o npm i son equivalentes a npm install, mientras que npm unlink, npm remove, npm rm o npm r son equivalentes a npm uninstall.

Una vez hemos creado e inicializado nuestro proyecto con NPM, debemos aprender a instalar y desinstalar dependencias de nuestro proyecto de forma correcta, que es lo que veremos a continuación.

## Buscar paquetes de NPM 
Pero antes de instalar un paquete, primero debemos encontrarlos. Los paquetes de NPM podemos buscarlos a través del buscador de NPM, disponible en la web NPMjs.com. No obstante, también podemos utilizar el buscador de linea de comandos de npm:
```` bash
$ npm search howler
````

Si finalmente encontramos un paquete en el que estamos interesados y queremos ver más información sobre él, podemos utilizar el comando npm show, que nos mostrará más información del paquete o librería:
````bash

howler@2.2.0 | MIT | deps: none | versions: 47
Javascript audio library for the modern web.
https://howlerjs.com

keywords: howler, howler.js, audio, sound, web audio, webaudio, browser, html5, ...
$ npm show howler
````
Una vez encontrado el paquete que buscamos, toca instalarlo.

## Instalar paquetes 
Para instalar un paquete en nuestro proyecto, simplemente debemos utilizar el comando npm install, situados en la carpeta de nuestro proyecto. Esto instalará dicho paquete y todas sus dependencias en la carpeta node_modules/, a la vez que actualiza el fichero package.json añadiendo el paquete y su versión como una dependencia del proyecto.

Existen varias formas de instalar un paquete:

````bash
npm install -D	--save-dev	# Instala el paquete en el proyecto, como dependencia de desarrollo.
npm install	--save-prod	# Instala el paquete en el proyecto, como dependencia de producción.
npm install -g	--global #	Instala el paquete en el sistema, sin asociarlo al proyecto.
````
Las dependencias de desarrollo son aquellos paquetes que necesitamos en un proyecto mientras estamos desarrollándolo, pero una vez tenemos el código generado del proyecto, no vuelven a hacer falta. Los paquetes instalados con el flag --save-dev o -D se instalan en esta modalidad, guardándolos en la sección devDependences del fichero package.json.

Por otro lado, las dependencias de producción son aquellos paquetes que necesitamos tener en la web final generada, como librerías Javascript necesarias para su funcionamiento o paquetes similares. Los paquetes instalados con el flag --save-prod, -P o directamente sin ningún flag se instalan en esta modalidad, guardándolos en la sección dependences del fichero package.json.

Es importante diferenciar ambas modalidades, aunque al principio es habitual no saber exactamente cuando se trata de un paquete de desarrollo y cuando un paquete de producción.

Veamos un ejemplo de instalación con ambos tipos de paquetes:
````bash
# Instala en modalidad de desarrollo el paquete "gh-pages"
$ npm install --save-dev gh-pages

+ gh-pages@3.1.0
added 50 packages from 12 contributors and audited 92 packages in 1.998s
# Instala en modalidad de producción la librería "Howler"
$ npm install howler

+ howler@2.2.0
added 1 package from 1 contributor and audited 93 packages in 1.615s
````
Observa que en ambos casos, se nos indica la versión del paquete instalada tras el carácter @.

En el primer caso estamos instalando el paquete gh-pages, una librería y comando CLI para desplegar fácilmente un proyecto en GitHub Pages. Como se trata de un paquete que no es necesario incluir en la web final (se utiliza en desarrollo para desplegar), pues lo instalamos con los flags --save-dev o -D.

En el segundo caso, estamos instalando el paquete Howler, una librería Javascript que permite manipular y gestionar archivos multimedia de audio desde el navegador. En este caso se trata de una librería JS que si estará incluida en la versión definitiva de la página, por lo que la instalaremos con el flag --save-prod, -P o sin indicar ninguno, ya que es la opción por defecto.

En la última modalidad los paquetes instalados de forma global no se asocian al proyecto, sino al sistema. Se explican en detalle en el capítulo Instalaciones globales con NPM.

## El comando npx 
Aunque hasta ahora hemos hablado de instalar paquetes de línea de comandos de forma global, también es posible instalarlos en el proyecto, y aquí es donde cobra vital importancia el comando npx.

Un problema que puede surgir es que si instalamos un paquete de linea de comandos a nivel de proyecto (y ya tenemos instalada otra versión más antigua en el sistema de forma global) tendrá preferencia esta última.

Es más, incluso si instalamos el paquete a nivel de proyecto solamente, es posible que al ejecutarlo el sistema no lo encuentre, ya que no está en el PATH del sistema, sino que está dentro de la carpeta node_modules/.bin.

Para solucionar esto, podemos ejecutar comandos CLI instalados de forma local de la siguiente forma:
````bash
# Instalamos el paquete parrotsay en el proyecto actual
$ npm install -D parrotsay

# Ejecutamos el comando "parrotsay"
$ npx parrotsay
````
Esta última linea es equivalente a escribir ./node_modules/.bin/parrotsay, pero obviamente, mucho más cómodo.

El comando npx hace lo siguiente:

1) Busca si el paquete está instalado en node_modules/.bin. Si lo está, lo ejecuta.
2) Si no está, lo buscará en el sistema (instalado de forma global). Si está, lo ejecuta.
3) Si no lo encuentra, lo instalará temporalmente y lo ejecuta.
Esto hace que sea muy cómodo utilizar npx para ejecutar comandos CLI rápidamente.

## Pasar desarrollo a producción 
Si tenemos un paquete ya instalado en la modalidad de desarrollo y nos damos cuenta que realmente queremos tenerlo en la modalidad de producción (o viceversa), no es necesario desinstalar y volver a instalar el paquete.

Simplemente, escribimos el comando de instalación de la modalidad a la que queremos pasar:
````bash
$ npm install --save-prod howler
````
Internamente, npm se encargará de modificar el package.json y cambiar el paquete ya instalado de la sección devDependences a dependences.

## Instalar versiones específicas 
Si en algún momento necesitamos instalar una versión específica de un paquete, podemos hacerlo indicando la versión tras el nombre del paquete, separándola mediante el carácter @:
````bash
# Muestra las versiones disponibles del paquete @vue/cli
$ npm show @vue/cli versions
...
  '4.4.0',          '4.4.1',          '4.4.2',          '4.4.3',
  '4.4.4',          '4.4.5',          '4.4.6',          '4.5.0'
]

# Instala la versión 4.4.6 de @vue/cli
$ npm install -D @vue/cli@4.4.6
````
Esto puede ser interesante en algunas situaciones cuando nos encontramos que actualizar a la última versión de un paquete, nuestro proyecto deja de funcionar, o porque no queremos tener instalada la última versión de una librería.

Nota: Quizás el nombre del paquete @vue/cli te pueda parecer extraño. Se trata de una buena práctica el utilizar el formato @namespace/paquete para nombrar paquetes. La palabra namespace se usa para el nombre del autor/producto/compañía y paquete para el nombre del proyecto.

## Desinstalar paquetes 
Si queremos desinstalar un paquete de nuestro proyecto, simplemente escribimos el siguiente comando en la terminal de texto:
````bash
npm uninstall howler
````
Esto se encargará de eliminar el paquete de node_modules/ y eliminar su asociación al proyecto en el package.json, independientemente de ser una dependencia de desarrollo o de producción.