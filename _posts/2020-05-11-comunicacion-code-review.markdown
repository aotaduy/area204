---
title:  "Comunicación y code review"
date:   2020-05-11 11:30:05 -0300
tags: software bestPractices codeReview
categories: software
toc: true
---
A la hora del code review puede ser dificil comunicar los resultados porque estamos haciendo una critica del trabajo de otros. 

El trabajo del code reviewer es encontrar probleamas y fallas en el código, eso es el centro del proceso pero debemos tener ciertos criterios a la hora de comunicar estos resultados ya que el que los recibe es otra persona y es importante que se mantenga una buena relación en el entorno de trabajo. 

## Como comunicar en el code review

Vamos a mostrar una lista de do's y dont's en el code review a la hora de comunicar los problemas en el código:

+ No referirse a la persona, referirse a uno mismo
    + Correcto: 'Me resulta dificil entender lo que hace esta función'
    + Incorrecto: 'Estas escribiedo funciones muy cripticas'
+ Incluirse como parte del arreglo del problema: 
    + Correcto: 'Deberiamos arreglar estos tests'
    + Incorrecto: 'Tenes que arreglar estos tests'
+ Criticar lo que hace el codigo, no al autor
    + Correcto: 'Creo que deberiamos arreglar estos tests'
    + Incorrecto: 'Sos un poco descuidado al escribir los tests'
+ Hablar del código no de la persona
    + Correcto: 'Esta función se llama muchas veces, parece inficiente'
    + Incorrecto: 'Estas llamando a la función muchas veces, parece inficiente'
+ Usar PID, Percepción, Impacto, Deseo
    + Percepción: 'Para mi este metodo es muy largo'
    + Impacto: 'Me dificulta entender realmente que hace'
    + Deseo: 'Lo dividiria en varios metodos privados, con buenos nombres'
+ Aceptar que hay diferentes soluciones para un problema: 
    + Correcto: 'Yo lo haria de otra manera, pero asi funciona'
    + Incorrecto: 'Yo siempre lo hago de otra manera, deberias hacer lo mismo que hice en xxx'
+ Distinguir entre buenas prácticas y gusto personal
    + Correcto: 'Realmente no me gusta BEM, pero me parece que aca deberias aplicarlo porque es asi en el resto del proyecto'
    + Incorrecto: 'Veo que no estas usando BEM, me parece bien es una porqueria'
+ Hacer compromisos y ser pragmatico:
    + Correcto: 'Creo que deberiamos hacer un refactor de esta clase, pero sino llegan ahora, dejemoslo para el proximo sprint'
    + Incorrecto: 'Esta clase necesita un refactor grande, no puedo aprobarlo sino se hace'
+ Elegir que batallas luchar: 
    + No señalar cada linea de código. 
    + No ser pedante. 
    + Contactar al autor de forma personal para explicar nuestro punto de vista si vemos que el codigo tiene muchos problemas. 
    + Enfocarse en los problemas mas importantes del código.     
+ Ofrecer ayuda para solucionar los problemas.
    + Agregar snippets de codigo con la solucion a un problema o links a soluciones y problemas comunes. 

## Actitud al hacer code review

Cuando hacemos code review estamos ayudando al autor del código y estamos ayudando a la organización a contar con un código mejor, con menos bugs, mas legible, mas mantenible y mas seguro.

En muchos casos el review es obligatorio, por lo que agregar un comentario con una aprobación o involucrarse en el proceso acelera la revision y acelera la puesta en producción de ese código, ya que otros revisores lo pueden hacer con mas confianza y ver mas detalles, por lo tanto dar el approve y mergear mas rápido.

No debemos caer ni promover la idea de que con los comentarios estamos dificultando el trabajo de los demás ya que con los comentarios estamos desnudando una realidad que ya existe en el código la hacemos visible y a partir de ahi forzamos a que se tome una decisión con respecto de ello. 

## Timidez en la revisión

Muchas veces somos timidos a la hora de revisar código y no ponemos comentarios por razones de jararquia, por falta de experiencia en la empresa o por inseguridades. Es mejor un comentario que se hace y que es desestimado que otro que no se formula ya que puede desnudar errores o ayudar al programador a entender otro punto de vista o revisar ciertas prácticas que pueden no ser entendidas facilmente por otros aunque sean correctas.

## Propiedad colectiva del código

Por eso es mejor impulsar una cultura horizontalista de propiedad colectiva del código, donde todos hacemos code review, todos comentamos sin distinción de titulos, arquitectos, senior, junior, backend, frontend, fullstack ya que como equipo todos somos dueños y por lo tanto responsables de lo que se manda a producción y se deja en los repositorios de código de la organización. 
