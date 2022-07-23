---
eleventyNavigation:
  key: crear-proyecto-npm
  parent: npm
title: Crear un proyecto con npm

ordre: 2
---
NPM (Node Package Manager) nos permite, entre otras cosas, gestionar las dependencias de un proyecto de modo que no tenemos que hacerlo manualmente, sino de una forma relativamente automática y controlada, acelerando el desarrollo y reduciendo el tiempo necesario para mantener nuestros proyectos.

En este primer artículo vamos a repasar el scaffolding (estructura de carpetas) de un proyecto de frontend y como crear desde cero un proyecto con NPM.

## Inicializar el proyecto 
El primer paso será acceder a nuestra carpeta de proyectos (por ejemplo, /home/manz/workspace) y una vez allí, crear la carpeta del proyecto actual e inicializarlo. Por lo tanto, nuestro primer paso debe ser elegir un buen nombre para la carpeta de nuestro proyecto:
````bash
# Accedemos a la carpeta de todos nuestros proyectos
$ cd /home/manz/workspace

# Creamos la carpeta de nuestro proyecto
$ mkdir frontend-project

# Accedemos a su carpeta raíz (carpeta inicial)
$ cd frontend-project
````
Aunque pueda parecer una tontería, es muy importante escoger un buen nombre para la carpeta del proyecto. Ese nombre se suele utilizar en el repositorio de GitHub o en la URL para publicarlo si lo subimos a GitHub Pages, por ejemplo.

Algunos buenos consejos sobre el nombre del proyecto:

A) Utiliza siempre minúsculas.
B) No utilices espacios en el nombre. Usa guiones en su lugar.
C) Evita el uso de carácteres especiales, signos de puntuación, etc...
Una vez en la carpeta raíz del proyecto, sería una buena idea preparar git con un git init para llevar el control de versiones del proyecto cuanto antes. Esto creará una carpeta oculta .git donde se guardará toda la información relativa a git:
````
# Inicializamos el control de versiones
$ git init
````
Inicializado repositorio Git vacío en /home/manz/workspace/frontend-project/.git/
````
# Añadimos la URL de GitHub (u otro servicio) como repositorio remoto
$ git remote add origin https://github.com/ManzDev/frontend-project.git
````
También sería un buen momento para crear un archivo .gitignore, que indique las carpetas que vamos a ignorar con git. La carpeta node_modules/ debe estar obligatoriamente en dicho fichero.

Una vez hecho esto, inicializamos el proyecto con NPM, escribiendo npm init -y. Esto creará un fichero llamado package.json del que hablaremos más adelante y que contendrá toda la información del proyecto:
````
# Inicializamos el proyecto con NPM
$ npm init -y

Wrote to /home/manz/workspace/frontend-project/package.json:

{
  "name": "frontend-project",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/ManzDev/test.git"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/ManzDev/test/issues"
  },
  "homepage": "https://github.com/ManzDev/test#readme"
}
````
El parámetro -y de npm init omite el asistente interactivo, creando el package.json con los valores por defecto directamente y sin preguntarnos. Si prefieres utilizar el asistente, omite ese parámetro.

Observa que es interesante crear primero el repositorio de git y añadir el remote, puesto que así el package.json generado con NPM ya tendrá las entradas repository, bugs y homepage. De hacerlo posteriormente, tendríamos que añadirlas a mano.

Crear la estructura de carpetas 
Para trabajar en un proyecto, es necesario conocer bien el scaffolding (o estructura de carpetas). Aunque esta estructura puede variar de un proyecto a otro, utilizaremos la siguiente, ya que considero que es bastante estándar y que puede servir como punto de partida:

- frontend-project/       # Carpeta raíz del proyecto
  - .git/                 # Carpeta oculta de datos de git
  - node_modules/         # Carpeta de paquetes de Node/NPM
  - dist/                 # Carpeta de código generado (cuando se usan preprocesadores)
  - src/                  # Carpeta de código fuente (código editable)
    - assets/             # Carpeta de estáticos (imágenes, audio, video, fuentes...)
    - js/                 # Carpeta de Javascript
      - index.js
    - css/                # Carpeta de CSS
      - index.css
    - index.html
  - package.json          # Archivo del proyecto NPM
  - package-lock.json     # Histórico de versiones de dependencias
  - .gitignore            # Ficheros y carpetas a ignorar por git

Hasta ahora, solo deberíamos tener la carpeta .git, el archivo package.json y el archivo .gitignore (si lo hemos creado). La carpeta node_modules se creará desde que instalemos al menos un paquete en el proyecto (no de forma global), por lo que no nos preocuparemos de ella de momento.

La carpeta dist se suele crear sólo en proyectos donde estamos utilizando preprocesadores, transpiladores o herramientas consideradas «build tools», que de momento no estamos usando.

Así pues, vamos a crear la estructura de carpetas src, de la que si debemos preocuparnos:
````
# Creamos las carpetas src y subcarpetas
mkdir -p src/{assets,js,css}

# Creamos los ficheros HTML, CSS y Javascript
touch src/index.html
touch src/js/index.js
touch src/css/index.css
````
Una vez creados los archivos, faltaría crear un código HTML de base en el index.html y enlazar correctamente al archivo index.css en una etiqueta <link> y al archivo index.js en una etiqueta <script>.

Servidor local simple 
Para terminar, sería interesante contar con un servidor local de desarrollo que nos muestre como se va viendo la página según vamos escribiendo el código. Existen múltiples de estos servidores locales, veamos algunos de ellos:

Servidor local	Descripción	D.S.
live-server	Un servidor de desarrollo HTTP con actualización a tiempo real	🔄💾250K
lite-server	Servidor local de desarrollo ligero para NodeJS. Usa BrowserSync.	🔄💾44K
sirv-cli	Servidor local de desarrollo ligero con interfaz CLI para servir sitios estáticos	💾26K
local-web-server	Servidor local de desarrollo modular para desarrollos rápidos FullStack	💾36K
http-serve	Un servidor local en línea de comandos	💾8K
Es cosa nuestra decidir instalar el servidor de desarrollo asociado al proyecto o instalarlo de forma global. En este ejemplo instalaremos live-server de forma global, ya que en los próximos capítulos veremos como hacerlo en el proyecto, algo quizás más apropiado.

Lo utilizaremos para montar un servidor local y ver todo el contenido de la carpeta src en un navegador, con cambios en tiempo real a medida que vamos escribiendo código:
````
$ npm install -g live-server

$ live-server src
Serving "src" at http://127.0.0.1:8080
Ready for changes
Al hacer esto, y pulsar en la URL http://127.0.0.1:8080, debería aparecernos la página que tenemos en nuestro index.html.
````
Servidor local avanzado 
A medida que avancemos en nuestros desarrollos, los servidores locales de desarrollo anteriores se nos irán quedando pequeños, e iremos necesitando características más potentes. Por ejemplo, es muy común empezar a utilizar build tools, tanto en la parte de CSS (LESS, Sass, PostCSS...) como en la parte de Javascript (Babel, TypeScript...), por lo que las herramientas anteriores se nos quedarán cortas.

Los siguientes servidores locales de desarrollo están preparados para tareas más complejas y se adaptarán mejor a nuestros casos si comenzamos a utilizar estas herramientas:

Servidor local + Automatizador	Descripción	D.S.
es-dev-server	Servidor local de desarrollo, ideal para WebComponents. Tutorial	🔄💾18K
parcel	Automatizador moderno, orientado a build tools y preprocesamiento.	🔄💾70K
webpack-dev-server	El más popular, extendido y utilizado, pero también el más complejo.	🔄💾10M
En la sección de WebComponents de LenguajeJS tienes, paso a paso, un detallado tutorial para aprender a utilizar es-dev-server, uno de los servidores locales de desarrollo mencionados en la tabla anterior.