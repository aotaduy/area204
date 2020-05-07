---
title:  "Eslint spellchecker"
date:   2020-03-01 09:34:05 -0300
tags: javascript eslint spellcheck typescript
categories: software
---
ESLint es un es un analizador de código para javascript que permite detectar errores estaticamente, problemas de estilo e inclusive arreglarlos de forma automática.

Este es un plugin para [ESLint](https://eslint.org/) Que hice hace varios años y que sirve para comprobar la ortografía dentro del codigo fuente javascript, lo interesante es que checkea la otrtografía en las palabras teniendo en cuenta el camelCase, snake-case o diferentes opciones de casing. También diferencia y busca dentro de strings y constantes. 

El repo y las instrucciones de instalación [aqui](https://github.com/aotaduy/eslint-plugin-spellcheck) (ingles).

Paquete npm (https://www.npmjs.com/package/eslint-plugin-spellcheck)

Lo hice cuando trabajaba con angularjs para verificar el codigo que estaba haciendo, principalmente para no meter errores ortográficos en ingles.

Desde el punto de vista del código es un ejemplo interesante de TDD y de programación javascript ES5, previa a la masificación del uso de clases de ES6 u otras herramientas como TypeScript.