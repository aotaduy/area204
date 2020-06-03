---
title:  "Angular - Unit tests, elementos y buenas practicas"
date:   2020-06-03 11:30:05 -0300
tags: software bestPractices unitTest angular
categories: software
toc: true
---

Angular es un framework que fue concebido con la testeabilidad como una prioridad, proporciona un esquema de inyección de dependencias y varias herramientas y helpers para facilitar la testeabilidad de la aplicación. 

En este articulo algunos elementos de unit test del framework y consejos prácticos para su implementación. 

El CLI de Angular nos da un esqueleto para los unit test y un tipico proyecto generado con el CLI ya integra jasmine y karma.

## Jasmine
[Jasmine](https://jasmine.github.io) es un framework para unit test que incluye métodos para la especificación de [Behavior Driven](https://en.wikipedia.org/wiki/Behavior-driven_development) Unit Test facilitar la creación de Spies, Stubs y Mocks (ver esta [cheatSheet](https://devhints.io/jasmine) o la [Doc](https://jasmine.github.io/api/2.9/global)) de [Jasmine](https://jasmine.github.io).
Muy recomendable leer esta [Intro](https://jasmine.github.io/2.0/introduction)

## Karma
[Karma](https://karma-runner.github.io/) es un test-runner, es un programa que se encarga de correr los tests en secuencia, implementa un watch para correr los test de forma continua mientras se desarrolla y se puede configurar para que corra los tests en diferentes navegadores (Chrome, ChromeHeadless, IE, Firefox, etc).

El archivo karma.conf.js nos permite configurar estos parámetros.

Lo mejor es configurar una tarea para correr los tests con ChromeHeadless siguiendo esta guia.
(https://angular.io/guide/testing#configure-cli-for-ci-testing-in-chrome)
Asi podemos usar esa misma tarea para correr en nuestro [CI](https://es.wikipedia.org/wiki/Integraci%C3%B3n_continua). 

## Archivos de Unit Test
Una buena practica es crear un archivo de unit test para cada elemento de angular (componente, directiva, pipe, service, etc) que tengamos, el archivo normalmente tiene el mismo nombre que el elemento seguido del sufijo `.spec.ts`

Ejemplo:
 
`app.component.ts => app.component.spec.ts `
`trim.pipe.ts => trim.pipe.spec.ts `
`analytics.service.ts => analytics.service.spec.ts `

Esto nos facilita ver que componentes tienen unit test y también que test corresponde con cual componente. 

### Localizacion de los archivos de unit test
Los archivos de unit test deben estar junto con los componentes que testean no es conveniente crear carpetas `test` o ramas enteras de carpetas con los tests por separado. De esta forma queda claro que componentes tienen sus unit test y cuales no, además de facilitar la navegacion cuando se estan desarrollando.

### Eliminar archivos de unit test vacíos.
No es conveniente mantener archivos de test que no hacen nada o que no funcionan. El CLI de angular genera por defecto un esqueleto de test ante cada componente, pero si no vamos a implementar el test correspondiente es mejor eliminarlo, junto con todo otro dead code.

Mas archivos en nuestro proyecto son mas archivos que mantener, refactorizar y que pueden inducir a errores.

Menos codigo es mejor codigo, el unico codigo perfecto es el que no existe. 

### Archivos minimos de unit test
Si queremos tener un nivel de cobertura minimo, deberíamos hacer un unit test de creación del componente que configure el modulo de test con las dependencias necesarias para el componentes y evalué que el componente se crea correctamente. Este es el primer paso para crear un unit test partiendo de una clase existente y muchas veces es lo mas tedioso y dificultoso ya que implica mockear o instanciar las diferentes dependencias de nuestra clase para tener un entorno de unit test valido.

La dificultad mayor de crear un unit test suele estar en esta etapa de inicialización una vez que tenemos el entorno es facil crear nuevos casos de prueba.

Es facil también una vez que tenemos nuestra clase instanciada en el entorno de test, crear algunos casos de prueba que representen el happy path de nuestro componente.

En componentes stateless y componentes simples esto representa muchas veces mas del 80% del coverage de nuestro codigo.

## Guia de Creacion de Unit test por tipo de componente
En la pagina de [Angular](http://angular.io) se pueden consultar una completa guia por tipo de elemento del framework con ejemplos para la creación de unit tests.
(https://angular.io/guide/testing)
+ [Por ejemplo para Servicios](https://angular.io/guide/testing#service-tests)
+ [Componentes con bindings (`@Input()`)](https://angular.io/guide/testing#component-binding)
+ [Componentes con servicios asincronos](https://angular.io/guide/testing#component-with-async-service)
y otros.

## Code Coverage
El code coverage es el porcentaje de nuestro codigo que se ejecuta cuando se corre el suite de unit test, es una estadística muy util y una herramienta muy importante para verificar que nuestros unit test son completos. 

Para habilitar el reporte de code coverage se puede usar:

`ng test --no-watch --code-coverage` 

Ver [aqui](https://angular.io/guide/testing#enable-code-coverage-reports) para mas detalles.
esto va a crear una carpeta `coverage` en nuestro repositorio con un reporte en html muy grafico que especifica cuantas veces se ejecuto cada linea y coloreando las lineas que no se ejecutaron.
![Code Coverage Report]({{ site.baseurl }}/assets/screenshots/coverage-helpers.png)

### Coverage Driven Unit Test
Una buena practica es mientras estamos desarrollando el unit test de una clase existente usar este reporte para crear nuevos casos de prueba que nos permitan cubrir mas lineas, funciones y branches del codigo.
Cuando hacemos esto es importante crear casos de prueba que se condigan con la realidad del uso de ese componente y no poner valores de entrada irreales con tal de probar tal o cual funcion o branch de nuestro codigo. 

### Objetivos y Parametros
Si tuviéramos que setear un standard, una buena practica seria que todos los componentes tengan su unit test funcionando y a una cobertura global del 80% de nuestro codigo. 
También a que los tests esten integrados a pre push hooks (ver [husky](https://github.com/typicode/husky)) en cada repositorio y a que se corran como parte de la integración continua en todos los proyectos.

### Mas info: 
+ [Documentacipn oficial testing angular](https://angular.io/guide/testing)
+ [TDD](https://es.wikipedia.org/wiki/Desarrollo_guiado_por_pruebas)
+ [Errores Frecuentes by Sol Lopez](https://solopez.github.io/jasmine/)
+ [Mas sobre TDD con ejemplos en JS](https://softwarecrafters.io/javascript/tdd-test-driven-development)
