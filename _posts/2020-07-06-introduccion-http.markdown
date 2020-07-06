---
title:  "Http - Introducción al protocolo"
date:   2020-07-06 11:10:07 -0300
tags: utn ttads video educación http
categories: educación
toc: true
---
El protocolo http es uno de los más usados del mundo, es una parte fundamental de la [www](https://es.wikipedia.org/wiki/World_Wide_Web).

Vamos a ver cuales son sus partes fundamentales desde el punto de vista de la comunicación entre partes de una aplicación como [backend y frontend](https://es.wikipedia.org/wiki/Front_end_y_back_end).
 
## Protocolo HTTP componentes y usos

El protocolo por defecto para trabajar en el browser, algunas características, usos, y elementos que lo componen.

{%include video id="sNKYI53A6wQ" provider="youtube" %}

## El Request :rocket:

Para obtener información sobre un recurso lo primero es enviar un request :rocket:. Este request tiene un verbo, una cabecera y un cuerpo. 
Veamos un detalle de cada una de las partes:
{%include video id="vKjT58lTuPQ" provider="youtube" %}

## El Response

Cada Request se corresponde con un Response :memo:, este también tiene varias partes similares a los del request :rocket:, una linea de estado, un codigo de estado, una cabecera de respuesta y un cuerpo. 

{%include video id="7LTUaDDryt0" provider="youtube" %}

## Ejemplos

Con un navegador web standard podemos examinar los detalles de la secuencia de request y response :recycle: que se producen al navegar por una pagina de internet o de una [SPA](https://es.wikipedia.org/wiki/Single-page_application). 

{%include video id="OhDIdoF4XEY" provider="youtube" %}

### Mas info de sobre Http y en particular su aplicación en Angular

Este post es parte de una serie de videos para la cátedra de [Técnicas y Tecnologías Avanzadas de Desarrollo de Software (TTADS)][ttads-github].
Sobre Angular, en este caso el funcionamiento básico del protocolo HTTP.

[Aca][ttads-presentacion] se puede ver la presentación que se usó para esas clases.


[Acá](https://www.youtube.com/channel/UCkRACqaN5XpgH0P5hyqpQEw/featured) el canal de youtube de la materia.

[ttads-github]: https://github.com/utnfrrottads/
[ttads-presentacion]: https://utnfrrottads.github.io/presentacion-angulario/#/
