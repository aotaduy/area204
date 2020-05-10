---
title:  "Angular Template"
date:   2020-05-03 09:30:05 -0300
tags: utn ttads video educacion angular javascript typescript
categories: educacion
toc: true
---
Una serie de videos para la catedra de [Tecnicas y Tecnologias Avanzadas de Desarrollo de Software (TTADS)][ttads-github].
Sobre Angular, en este caso las directivas basicas del framework. 

[Aca][ttads-presentacion] se puede ver la presentacion que se uso para esas clases.

[La documentación oficial de Angular](https://angular.io/docs) la base para empezar a usar el framework.


## Angular Binding de Atributos	

En angular podemos pasar parametros a otros tags con los resultados de algun calculo de nuestro componente, para eso tenemos el binding de atributos. 

{%include video id="1oxWTlQVBM8" provider="youtube" %}

## Angular Binding de Eventos

Para poder tomar entradas de los gestos del usuario en la interfaz podemos conectar los eventos del DOM con llamadas a metodos de nuestros componentes, por ejemplo un click en un boton, el puntero del mouse ingresando en un div, o la presion de una tecla.

Con el binding de eventos podemos lograr este comportamiento.

{%include video id="E7Zj3nEXjQY" provider="youtube" %}

## Angular Directivas del Framework

Angular provee varias directivas basicas que permiten cierto flujo de control dentro del Template, con ellas podemos eliminar o incluir ciertas partes del DOM, iterar sobre una coleccion y generar elementos, o agregar y eliminar clases y estilos CSS en base a diferentes condiciones. 

### Angular NgIf, NgClass, NgStyle

Condiciones para incuir o eliminar elementos, clases y estilos. 

{%include video id="sVUHTZhk3XU" provider="youtube" %}

### Angular NgFor

Iterar sobre colecciones y generar elementos

{%include video id="tw3tWMLDzsw" provider="youtube" %}


## Angular Ejemplo completo con directivas del framework

En este ejemplo creamos un componente Con una lista de Tareas por hacer en un unico componente con las directivas del framework. 

{%include video id="i7IQej0Zomk" provider="youtube" %}


[ttads-github]: https://github.com/utnfrrottads/
[ttads-presentacion]: https://utnfrrottads.github.io/presentacion-angulario/#/
