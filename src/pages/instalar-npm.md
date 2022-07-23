---
eleventyNavigation:
  key: instalar-npm
  parent: npm
title: Instalar npm

ordre: 1
---
***NPM*** son las siglas de ***Node Package Manager***, es decir, gestor de paquetes de NodeJS, un entorno de ejecución multiplataforma para ejecutar Javascript no sólo en un navegador web (como se concibió originalmente) sino fuera de él, y poder utilizarlo en sistemas de escritorio o servidores web.

Este gestor de paquetes (muy similar al concepto de apt-get en GNU/Linux), nos permitirá instalar de forma muy sencilla y automática paquetes Javascript (tanto de Node como Javascript para el navegador) y utilizarlo para nuestros fines.



## Instalación de npm (windows) instalando node
Para comenzar, necesitaremos instalar NodeJS en su versión LTS (recomendada) . Al instalar Node, se instalará automáticamente su gestor de paquetes .
![Descargar Node para windows](/eleventy/img/node.jpg)

Luego podemos comprobar si tenemos NodeJS/NPM instalado y que versión tenemos:
````bash
# Muestra la versión de Node
$ node --version

# Muestra la versión de NPM
$ npm --version
````
En el caso de que no tengamos node instalado en nuestro sistema, se nos mostrará un mensaje de error como node: command not found o similar, en cuyo caso deberemos proceder a instalarlo (necesitaremos tener privilegios de root o permisos de sudo).

En el caso de tener una versión muy antigua, también podemos realizar los pasos que veremos a continuación y aprovechar para actualizarlo.



## ¿Para que usaremos NPM? 
Ahora que tenemos node y su gestor de paquetes npm disponible en nuestro sistema, podremos instalar paquetes de NPM en nuestros proyectos y/o en nuestro sistema.

Hay 2 modalidades principales para utilizar NPM:

- A nivel de proyecto: Probablemente la modalidad más utilizada es la de usar NPM como un gestor de dependencias de un proyecto, esto es, un sistema con el que controlamos que paquetes o librerías Javascript están instalados (y que versión), de modo que quedan asociados al proyecto en sí. Esto facilita que si un usuario diferente se descarga el proyecto, pueda gestionarlo fácil y rápidamente (instalar paquetes, actualizarlos, etc...)

- A nivel global: Existen algunas situaciones específicas, en las que los paquetes son realmente utilidades que no se utilizan en proyectos, muy común en aplicaciones de línea de comandos (CLI) que usamos desde terminal. En esta modalidad, los paquetes se instalan a nivel del sistema (no en la carpeta del proyecto), por lo que están disponibles siempre que el usuario quiera utilizarlos, sin necesidad de tenerlo en cada proyecto.