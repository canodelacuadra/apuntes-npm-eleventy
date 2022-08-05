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
 inicializamos el proyecto con NPM, escribiendo npm init -y. Esto creará un fichero llamado package.json del que hablaremos más adelante y que contendrá toda la información del proyecto:
````bash
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



