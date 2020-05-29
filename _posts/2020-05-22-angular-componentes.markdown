---
title:  "Angular Componentes"
date:   2020-05-22 09:30:05 -0300
tags: utn ttads video educación angular javascript typescript
categories: educación
toc: true
---
El bloque básico de construcción de Angular son los componentes, un componente tiene una clase y un template asi como atributos de entrada y salida. 


## Angular Input

En Angular el bloque básico de construcción son los componentes, la aplicación es un componente, una lista es un componente, un formulario es un componente, etc. 

Para poder rehusar esos componentes se pueden parametrizar, la forma mas común de hacerlo es a través de inputs. 

Un Input define un parámetro que le puedo pasar al componente omo si fuera un atributo de un tag html.
 
{%include video id="Hvk-wH0ufxg" provider="youtube" %}

## Angular Output
Asi como tienen entradas los componentes de angular pueden definir eventos de salida, asi el componente padre puede reaccionar a lo que pasa dentro del componente. 

De esta forma un componente comunica que algo esta pasando y diferentes usuarios de ese componente pueden reaccionar a estas salidas de acuerdo a su necesidad.

Se sigue un patron [Observer](https://es.wikipedia.org/wiki/Observer_(patr%C3%B3n_de_dise%C3%B1o)) y de esta forma se pueden comunicar de forma desacoplada dos componentes.

{%include video id="FUeq0ZOZwX0" provider="youtube" %}

## Ejemplo

Mostramos un ejemplo de uso de estas propiedades. Y un ejercicio muy basico.
En este [repo](https://github.com/utnfrrottads/angular9-example/tree/todo-list-exercise) esta la consigna y en las [pull request](https://github.com/utnfrrottads/angular9-example/pulls) se pueden ver varias resoluciones alternativas 

{%include video id="87H0y9V-4rE" provider="youtube" %}

### Proyección de Contenido

Además de la  entrada por input un componente puede recibir un template como con otros componentes para renderizarlos en su interior.

A esto se le llama proyección de contenido, es el comportamiento estandar de los tags de html como div, p y otros que muestran lo que esta contenido entre el tag de inicio y fin. 

En angular podemos hacer lo mismo con nuestros componentes (aunque no es el comportamiento por defecto).
{%include video id="glAwIxmKzd0" provider="youtube" %}

### Ciclo de vida de un componente

Los componentes tienen un ciclo de vida bien definidos, existen hooks que un componente puede implementar para "engancharse" a los diferentes momentos del ciclo de vida de un componente:

Los mas importantes son: 

+ `ngOnInit` para inicializar
+ `ngOnChanges`cuando cambia un objeto de los @Input
+ `ngOnDestroy` cuando se elimina el componente del DOM

en el video detallamos el resto y se da una explicación y demostración de los mismos

{%include video id="EJl3zuDeGwo" provider="youtube" %}

### Mas info de Angular

Este post es parte de una serie de videos para la cátedra de [Técnicas y Tecnologías Avanzadas de Desarrollo de Software (TTADS)][ttads-github].
Sobre Angular, en este caso el funcionamiento básico de los componentes, input, output, y el ciclo de vida.

[Aca][ttads-presentacion] se puede ver la presentacion que se uso para esas clases.

[La documentación oficial de Angular](https://angular.io/docs) la base para empezar a usar el framework.

[Acá](https://www.youtube.com/channel/UCkRACqaN5XpgH0P5hyqpQEw/featured) el canal de youtube de la materia.

[ttads-github]: https://github.com/utnfrrottads/
[ttads-presentacion]: https://utnfrrottads.github.io/presentacion-angulario/#/
