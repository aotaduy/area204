---
title:  "Angular Servicios"
date:   2020-06-11 17:30:07 -0300
tags: utn ttads video educación angular javascript typescript
categories: educación
toc: true
---
Los servicios son elementos no visuales dentro de Angular, se usan para compartir funcionalidad, comunicar componentes y ordenar el código. 

## Servicios e Inyección de Dependencias

En Angular podemos especificar servicios que son básicamente clases que la mayoria de las veces actuan como [singletons](https://es.wikipedia.org/wiki/Singleton).

Generalmente contienen cierta funcionalidad o estado compartido entre diferentes componentes. 

Angular tiene un sistema de inyección de dependencias totalmente integrado en el framework. Este sistema implementa la Inversion de Control en la instanciación de nuestros servicios para desacoplarlos y entre otras cosas facilitar el testing.

{%include video id="hRyZhcUqjrk" provider="youtube" %}

## Servicios introducción
Para crear un servicio podemos usar el `angular/cli` para generarlo y con uns simple Inyección empezar a utilizarlo.

``ng generate service Todo ``

por ejemplo va a generar la clase `TodoService` con un esqueleto de unit test.

{%include video id="jsN2iNPr7ik" provider="youtube" %}

## Modos de Inyección de servicios
Vamos a ver tres formas bascas de inyectar un servicio: 
+ En el modulo root
+ En un modulo particular
+ En un componente

Cada una opera de forma ligeramente diferente en cuanto a las instancias generadas por el inyector. 
En el primer caso un [singleton](https://es.wikipedia.org/wiki/Singleton), en el segundo un singleton a nivel modulo, diferentes modulos tendran diferntes instancias, y en el tercero el servicio acompaña el ciclo de vida del componente.

{%include video id="h1epK7q2Jpc" provider="youtube" %}

## Servicios ¿para que?  

Existen muchas razones para usar servicios entre otras: 

+ Agrupar funcionalidad compartida
+ Comunicar componentes
+ Ordenar mejor el código

Veremos en detalle con un ejemplo como hacer cada una. Mientras hacemos un refactor de nuestra humilde  TodoList
{%include video id="ei77W5FRMV8" provider="youtube" %}

### Ejercicios
Un ejercicio para practicar nuestro conocimiento sobre TodoList.

Tomar el codigo del branch [servicios](https://github.com/utnfrrottads/angular9-example/tree/services) bajarlo a su propio repo e implementar en otro servicio llamado LocalStorageService el guardado de la lista de forma persistente segun las apis del navegador
+ [JSON stringify](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/JSON/stringify)
+ [JSON parse](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/JSON/parse)
+ [LocalStorage](https://developer.mozilla.org/es/docs/Web/API/Storage/LocalStorage)


{%include video id="HWrLtPiZAxs" provider="youtube" %}


### Mas info de Angular

Este post es parte de una serie de videos para la cátedra de [Técnicas y Tecnologías Avanzadas de Desarrollo de Software (TTADS)][ttads-github].
Sobre Angular, en este caso el funcionamiento básico de los servicios e inyección de dependencias.

[Aca][ttads-presentacion] se puede ver la presentacion que se uso para esas clases.

[Aca](https://github.com/utnfrrottads/angular9-example/tree/services) el codigo de este ejemplo.

[La documentación oficial de Angular](https://angular.io/docs) la base para empezar a usar el framework.

[Acá](https://www.youtube.com/channel/UCkRACqaN5XpgH0P5hyqpQEw/featured) el canal de youtube de la materia.

[ttads-github]: https://github.com/utnfrrottads/
[ttads-presentacion]: https://utnfrrottads.github.io/presentacion-angulario/#/
