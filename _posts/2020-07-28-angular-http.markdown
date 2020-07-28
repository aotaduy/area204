---
title:  "Angular - Http"
date:   2020-07-28 09:15:07 -0300
tags: utn ttads video educación http
categories: educación
toc: true
---
Como hacer llamadas http, get, post y mas para comunicarnos con el backend. 

Cuando trabajamos con [Angular](https://www.angular.io) generalmente necesitamos comunicarnos con otros sistemas o con el propio [backend](https://es.wikipedia.org/wiki/Front_end_y_back_end) de nuestro sistema.

Para entender  la comunicación [http]({% post_url 2020-07-06-introduccion-http%})  

:rocket: Vamos a ver cuales son los servicios que proporciona Angular para usarlo.
 
## Angular HTTP y Observables

:recycle: En angular las llamadas http y sus respuestas se realizan de forma asíncrona usando abstracciones de Reactive programming en particular, [RxJS](https://rxjs-dev.firebaseapp.com/) con los observables.

{%include video id="t82ElgKlYdU" provider="youtube" %}

## Http Manejo de errores y opciones

:monorail: Las llamadas post, get y otras se hacen por defecto como [json](https://es.wikipedia.org/wiki/JSON), pero se pueden definir otras opciones. 
Veamos un detalle:
{%include video id="tiC-pGBRYRU" provider="youtube" %}

## Ejemplos

### Primer ejemplo
:wrench: Un primer ejemplo de como configurar nuestro proyecto para usar http con la aplicacion de [real world app](https://github.com/gothinkster/realworld): 

{%include video id="5JgBsyST62A" provider="youtube" %}

### Mejorando el ejemplo

:electric_plug: Un ejemplo de POST y autenticación con un usuario hardcodeado .

{%include video id="lCpQ95VPWBY" provider="youtube" %}

### Ejercicio

:hammer: Un ejercicio para practicar lo que estuvimos aprendiendo. 

{%include video id="0clBCd2UYwg" provider="youtube" %}

## Más información 

Este post es parte de una serie de videos para la cátedra de [Técnicas y Tecnologías Avanzadas de Desarrollo de Software (TTADS)][ttads-github].
Sobre Angular, en este caso el funcionamiento básico de la biblioteca de Angular para HTTP.

[Aca][ttads-presentacion] se puede ver la presentación que se usó para esas clases.


[Acá](https://www.youtube.com/channel/UCkRACqaN5XpgH0P5hyqpQEw/featured) el canal de youtube de la materia.

[ttads-github]: https://github.com/utnfrrottads/
[ttads-presentacion]: https://utnfrrottads.github.io/presentacion-angulario/#/
