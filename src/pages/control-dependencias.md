---
eleventyNavigation:
  key: control-dependencias
  parent: npm
title: Control de dependencias

ordre: 5
---
Una dependencia es una aplicación o una biblioteca requerida por otro programa para poder funcionar correctamente.

En un programa las dependencias crecen, se actualizan y evolucionan, añadiendo nuevas funcionalidades, corrigiendo problemas, y quizás hasta puede que perdiendo funcionalidades por el camino.

Es por todos estos factores por lo que conviene y es importante aprender una serie de buenas prácticas para mantener nuestro proyecto en buen estado, y que mencionaremos.

## Versionado semántico
La forma más habitual de versionar nuestros paquetes es usando **versionado semántico**. Este tipo de versionado se basa en unas pautas concretas para determinar el número de versión de los paquetes o proyectos.

 Dado un número de versión de un proyecto, este número está formado por 3 partes, por ejemplo: a.b.c:

Tomemos por ejemplo que la  versión es 2.0.4:

* 2 es el **major version**. Se trata del número de versión mayor y se avanza uno más si las novedades del paquete, librería o proyecto van a producir cambios importantes  que no son compatibles con versiones anteriores. Si avanzaramos, pasaríamos a 3.0.0. Si tu paquete no está siendo usado en producción, se suele empreza con la versión 0. Empezar con la versión 0.1.0 en lugar de la 1.0.0.

* 0 es el **minor version**. Se trata del número de versión menor y se avanza uno más si las novedades del paquete, librería o proyecto introducen nuevas funcionalidades que son compatibles con versiones anteriores. Si avanzaramos, pasaríamos a 2.1.0.

* 4 es el **patch version**. Se trata del número utilizado para parches que corrigen problemas, bugs o defectos en funcionalidades del código actual y son compatibles con versiones anteriores. Si avanzaramos, pasaríamos a 2.0.5.

Por lo tanto, sabiendo estas características, observando el número de versión actual 2.0.4 y suponiendo que partimos de una primera versión 1.0.0, sabemos que desde el lanzamiento de la v2 ha tenido 5 parches para corregir errores o problemas.

Si quieres obtener más información sobre versionado semántico, puedes consultar la página oficial semver.org, donde tienen algunas recomendaciones.

## Dependencias del proyecto y Control de dependencias  
La lista de dependencias del proyecto se guardan en el **package.json**, en un apartado dependencies y en otro devDependencies, dependiendo si son paquetes de producción o de desarrollo respectivamente. 

Habrás observado que el número de versión de cada paquete, en algunas ocasiones viene precedido por un carácter especial, como ^ (circunflejo) o ~ (virgulilla). La ausencia o presencia de estos carácteres, junto a otros detalles, indica a npm como debe controlar el proceso de actualizaciones.

Para entenderlo mejor, imagina el siguiente supuesto (no es real al 100%, luego explicaré por qué):

Hoy, creamos un proyecto en el que instalaremos dos dependencias: A y B.
Al instalarlas con npm install ``<paquete>`` se instala la última versión disponible.
En el caso de A, se instala la versión 1.0.3. En el caso de B, la 1.4.0.
Todo funciona correctamente. Guardamos en GitHub y borramos el repo del equipo.
Retomamos el proyecto 3 meses después. Clonamos y hacemos un npm install.

* Se instala la última versión disponible de cada dependencia.
* En el caso de A, la última versión es 1.0.15. En el caso de B, la 2.2.1.

La dependencia A sigue funcionando correctamente, ya que sólo han habido parches.

La dependencia B falla, ya que el proyecto fue diseñado para la 1.4.0, y la versión 2.2.1 introduce cambios grandes que no son compatibles.

Sin haber cambiado ni una línea de código, nuestro proyecto está fallando, y esto ocurre porque los cambios externos a nuestro código también influyen en nuestro proyecto. Cada vez que añadimos una dependencia a nuestro proyecto, como su propio nombre indica, dependemos también de esa librería, código o sistema.

> IMPORTANTE: Para evitar situaciones como estas, npm incluye un ^ (circunflejo) antes del número de versión de la dependencia. De esta forma, sabemos que versión se instaló por primera vez, pero npm buscará la versión más alta disponible, teniendo en cuenta sólo parches y actualizaciones menores, pero nunca instalando actualizaciones mayores.

## Política de actualizaciones 
Si echamos un vistazo a las versiones de las dependencias de nuestro proyecto, veremos que tienen uno de los siguientes formatos:

- 1.2.4	Instala siempre la versión indicada 1.2.4.
- ^1.2.4	Instalará la versión menor más alta, sin llegar a pasar a la versión 2.x ni superiores. Por defecto.
- ~1.2.4	Instalará sólo los parches, sin llegar a pasar a la versión 1.3 ni superiores.
También es posible utilizar el carácter x o * para indicar comodines en la versión. Por ejemplo, la versión 1.2.x sería equivalente a ^1.2.0, la versión 1.x sería equivalente a ^1.0 y la versión * o x sería equivalente a cualquier versión. Puedes utilizar la «calculadora» de semver.npmjs.com para hacer pruebas y comprender el funcionamiento del versionado semántico.

Podemos controlar la versión que se instalará y la política de actualizaciones dependiendo de como instalemos los paquetes:
````bash
# Busca e instala la última versión disponible (usará ^2.3.1)
# (sólo permitirá actualización de versiones menores y parches)
$ npm install lit-element

# Instala la versión exacta 2.3.1
# (no permitirá actualizaciones a otras versiones)
$ npm install lit-element@2.3.1
````
Recuerda que siempre puedes editar manualmente el package.json y cambiar el caracter de versión si así lo deseas.

## Actualización de dependencias 
NPM tiene un sistema de actualización de dependencias integrado. Puedes activarlo ejecutando npm outdated, lo que mostraría algo parecido a lo siguiente:
````bash
$ npm outdated
Package      Current  Wanted  Latest  Location
gh-pages       0.4.0   0.4.0   3.1.0  frontend-project
lit-element    2.0.1   2.3.1   2.3.1  frontend-project
````
Este menú nos mostrará las dependencias que tienen actualizaciones. En la columna current la versión instalada en el proyecto, en la columna wanted la versión máxima determinada por nuestro versionado semántico del package.json y en latest la última versión disponible de la dependencia. Además, los colores (aunque bajo mi opinión, no muy adecuados) son importantes:

En rojo se nos mostrarán los paquetes que encajan con nuestra política de actualizaciones semver y podemos actualizar.
En amarillo se nos mostrarán los paquetes que no encajan con nuestra política de actualizaciones.
Sin embargo, existe un paquete no oficial llamado npm-check que mejora considerablemente el sistema de actualización de dependencias de NPM, con un sistema interactivo, mucha información bien desglosada y algunos parámetros interesantes:


- -u	Abre el menú interactivo de actualización. SPACE seleccionas paquetes y ENTER actualiza selección.
- -y	No abre menú interactivo, sino que actualiza todo sin preguntar.
- -p	No actualiza las dependencias de desarrollo, sólo las de producción.
- -d	No actualiza las dependencias de producción, sólo las de desarrollo.
- -g	Actualiza los paquetes globales del sistema, no los del proyecto.

Así pues, para actualizar las dependencias de nuestro proyecto, tras instalarlo de forma global con npm install -g npm-check, podemos ejecutarlo en modo interactivo con un simple npm-check -u:
````
npm-check: Actualizador de dependencias de NPM
``````
Observa que npm-check separa las actualizaciones en grupos de parches, versiones menores y versiones mayores, mostrando el número de versión actual y a actualizar, el texto devDep si es una dependencia de desarrollo, e incluso un enlace clickeable al README o la página de la dependencia para revisar los cambios.