---
eleventyNavigation:
  key: scripts-npm
  parent: npm
title: Scripts de npm

ordre: 6
---
A medida que trabajamos con nuestro proyecto, es muy habitual crear comandos para automatizar tareas. NPM proporciona un sistema denominado scripts de NPM, que es algo así como una colección de tareas de línea de comandos. Los que provienen de desarrollos más tradicionales como C o C++, puede que vean un símil con los scripts de tipo Makefile.

La idea es incorporar en el fichero package.json, una colección de scripts que pueden ser abreviados con un nombre de tarea y ejecutados desde una la carpeta raíz del proyecto escribiendo npm run <tarea>.

Estructura de los scripts de NPM 
Si echamos un vistazo al package.json, en su sección scripts, veremos que npm crea un apartado de scripts donde solo tenemos un script llamado test. Este script, por defecto no realiza ninguna tarea, simplemente es una llamada a echo mostrando que no existen tests:

$ cat package.json | jq .scripts
{
  "test": "echo \"Error: no test specified\" && exit 1"
}
Este script se puede modificar (o borrar) con seguridad, ya que no hace nada, pero lo interesante es crear nuevos scripts con tareas que relizamos frecuentemente. Veamos los nombres de tareas más comunes que se suelen utilizar:

Tarea	Descripción	Comando
start	Se suele usar para tareas de inicio del proyecto. Se puede arrancar con npm start.	npm run start
dev	Alternativa al anterior, se suele usar para levantar servidores de desarrollo locales.	npm run dev
serve	Idem al anterior.	npm run serve
build	Tarea que construye los ficheros finales para subir a la web de producción.	npm run build
test	Suele iniciar una batería de tests. Se puede arrancar con npm test o npm t.	npm run test
deploy	Suele desplegar en la web de producción la webapp construída con build.	npm run deploy
Obviamente, el desarrollador puede usar el nombre de tarea que más le guste (e incluso inventar otros), pero para tareas comunes como las mencionadas es una buena práctica utilizar alguna de las anteriores, ya que cualquier desarrollador ajeno al código sabrá lo que hace con solo leer su nombre.

Así pues, a modo de ejemplo, así quedarían los scripts de un package.json de un proyecto utilizando el automatizador parcel para desplegar en GitHub Pages:

"scripts": {
  "start": "parcel src/index.html",
  "build": "parcel build src/index.html -d build --public-url /frontend-project/",
  "deploy": "gh-pages -d build"
}
También es posible incluir los comandos de build y de deploy en una misma tarea, uniéndolos con &&, lo que en terminal significa: «si el comando anterior termina correctamente, ejecuta el siguiente», aunque esto puede complicar la legibilidad de los scripts.

Ejecutar scripts 
Como ya hemos mencionado, basta con ejecutar npm run <tarea> para ejecutar un script concreto de nuestro package.json. Si no recordamos los nombres de los scripts o estamos trabajando en un proyecto ajeno del que aún no conocemos los scripts, podemos ejecutar el comando npm run (sin nombre de tarea) y nos mostrará las tareas disponibles:

# Muestra los scripts incluidos en el package.json
$ npm run

# Muestra los scripts literalmente del package.json
$ cat package.json | jq .scripts
También es posible utilizar el comando ntl (npm task list) para utilizar un menú de texto y seleccionar la tarea de una forma más interactiva. Para ello, sólo tenemos que escribir npx ntl:

ntl: NPM Task List

Observa que con esta herramienta, podemos movernos con los cursores a través de los scripts que nos aparecen en el menú, seleccionando el que queramos ejecutar pulsando ENTER.

Preparación y finalización 
A medida que vamos creando scripts, es posible que queramos realizar tareas concretas antes o después de ejecutar un script determinado. Esto es posible simplemente creando una tarea con el prefijo pre o el prefijo post respectivamente.

Veamoslo con el ejemplo anterior:

"scripts": {
  "start": "parcel src/index.html",
  "predeploy": "parcel build src/index.html -d build --public-url /frontend-project/",
  "deploy": "gh-pages -d build"
}
El script deploy sube a GitHub Pages el contenido de la carpeta build. Como queremos que esté actualizada, creamos un script predeploy (que se ejecutará antes) y que ejecutará parcel para generar el contenido de esa carpeta build antes de subirlo, y de este modo esté todo actualizado.

De la misma forma se podría hacer con el prefijo post para tareas posteriores de finalización.

Organización y scripts en paralelo 
Conforme vamos creando scripts en el package.json, nuestra sección de scripts se puede ir complicando y haciendo más grande, por lo que conviene mantenerla organizada. Además, también puede entrar en juego la necesidad de crear scripts que ejecuten múltiples tareas de forma simultánea, o crear comandos que funcionen en sistemas como GNU/Linux y Mac, pero también en Windows. Para todo ello, existe un paquete llamado npm-run-all que nos permite realizar esto, entre otras cosas.

Uno de los principales objetivos de paquetes como npm-run-all o cross-env era simplificar la gestión de comandos entre sistemas operativos, evitando las diferencias que existen entre comandos UNIX y Windows. Actualmente, recomiendo utilizar Node/NPM a través de Windows Subsystem for Linux (WSL), lo que evita toda esta problemática.

Lo primero, es instalar el paquete npm-run-all en nuestro proyecto. Lo instalaremos como dependencia de desarrollo, puesto que es para gestionar proyectos NPM y no tiene relación con la web definitiva en producción:

$ npm install --save-dev npm-run-all
Una vez instalado, si necesitamos que se ejecuten múltiples tareas que queremos realizar de forma independiente podemos agruparlas con un namespace utilizando los dos puntos : y luego ejecutar el grupo entero con un npm-run-all <namespace>:*:

"scripts": {
  "build": "npm-run-all build:*",
  "build:html": "pug src/index.pug ...",
  "build:css": "postcss src/index.css ...",
  "build:js": "rollup src/index.js ..."
}
Por defecto, estas tareas se ejecutan secuencialmente. Es decir, hasta que la primera no termine, no se ejecutará la siguiente. Esto puede ser alterado utilizando el flag -p (parallel) a npm-run-all:

"scripts": {
  "dev": "npm-run-all -p dev:*",
  "dev:html": "pug --watch src/index.pug ...",
  "dev:css": "postcss --watch src/index.css ...",
  "dev:js": "rollup --watch src/index.js ..."
}
Automatizadores (tooling) 
Recuerda que los scripts de NPM no son más que un sistema para simplificar sencillas órdenes de línea de comandos. En el caso de que nuestros scripts se compliquen demasiado (o resulten demasiado «verbose») lo ideal sería buscar un automatizador de tareas o bundler que se adapte a nuestro proyecto y utilizarlo junto a los scripts de NPM.

En la siguiente tabla puedes observar varios de los más populares actualmente:

Herramienta	Descripción
Webpack	El automatizador por excelencia en el mundo Javascript. Complejo y avanzado.
Parcel	Automatizador moderno, orientado a simplicidad y comodidad. Aún en fase experimental.
Rollup	El automatizador por excelencia de los estándares. Soporta ESM y es muy eficiente.
Gulp	Automatizador de tareas orientado a código. Funciona de forma similar a los pipes de terminal.
Grunt	Automatizador de tareas orientado a ficheros. Algo obsoleto a favor de Gulp.
Browserify	Automatizador para crear bundlers para el navegador.
Snowpack	Automatizador orientado a simplificar las complejos worlflows de las build tools.
Just	Automatizador de tareas de Microsoft. Muy parecido a Gulp.
FuseBox	Automatizador para crear bundlers en Javascript.
En la excelente página Tooling.Report tienes más información sobre las diferencias de herramientas de este tipo, más concretamente, entre browserify, parcel, rollup y webpack.