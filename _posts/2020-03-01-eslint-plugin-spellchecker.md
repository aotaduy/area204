---
title:  "ESLint Ortografía en el código"
date:   2020-03-01 09:34:05 -0300
tags: javascript eslint spellcheck typescript opensource
categories: software
---
ESLint es un es un analizador de código para javascript que permite detectar errores estaticamente, problemas de estilo e inclusive arreglarlos de forma automática.

## ESLint plugin 

eslint-plugin-spellcheck es un plugin para [ESLint](https://eslint.org/) Que hice hace varios años y que sirve para comprobar la ortografía dentro del codigo fuente javascript, lo interesante es que checkea la otrtografía en las palabras teniendo en cuenta el camelCase, snake-case o diferentes opciones de casing. También diferencia y busca dentro de strings y constantes. 

## Configuración

Tiene varias opciones de configuración para permitir que algunas palabras tipicas del código no se tomen como errores de ortografía.

## Repo y paquete

El repo y las instrucciones de instalación [aqui](https://github.com/aotaduy/eslint-plugin-spellcheck) (ingles).

Paquete npm (https://www.npmjs.com/package/eslint-plugin-spellcheck)

## Motivación
Lo hice cuando trabajaba con angularjs para verificar el codigo que estaba haciendo, principalmente para no meter errores ortográficos en inglés.

Desde el punto de vista del código es un ejemplo interesante de TDD y de programación javascript ES5, previa a la masificación del uso de clases de ES6 u otras herramientas como TypeScript.

## Planes a futuro
La gente de typescript anunció hace poco que iban a favorecer el uso de [ESLint](https://eslint.org/) por sobre tslint por lo que este plugin vuelve a tener relevancia en los proyectos en los que estoy trabajando (principlamente Angular) asi que voy a volver a darle mantenimiento tratando de que funcione con typescript y angular.
