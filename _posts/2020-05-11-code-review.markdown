---
title:  "Revisión de código (code review)"
date:   2020-05-11 10:30:05 -0300
tags: software bestPractices codeReview
categories: software
toc: true
---
Si queremos asegurar la calidad, seguridad y mantenibilidad del software el code review debe formar una parte fundamental dentro del proceso de desarrollo. 

La revision de código o code review, consiste en la lectura del código fuente de un sistema con la finalidad de encontrar errores, problemas de seguridad, formato estilo o nomenclatura. 

## Cuando se hace
Se puede realizar sobre porciones del código o cambios antes de ser incorporados al trunk principal de desarrollo, como checkpoints en determinados momentos del proceso de desarrollo, como parte de una auditoria o sobre toda la base de código antes de una entreaa o como parte de la validación de la calidad de un entregable de software.

## Entrada

Como entrada para este proceso deberíamos tener: 
+ La base de codigo: código fuente, estilos css, scripts de sql, acceso a los repositorios.
+ Reglas de estilo: Las reglas de estilo que se usaron en el desarrollo. 
+ Principios de diseño: una descripción de los principios de diseño que se usaron para el desarrollo, los conceptos, arquitecturas, teorias y/o patrones involucrados. 

## Salida
La salida de este proceso es una seria de comentarios y recomendaciones, normalmente con el detalle de la linea concreta en el código, para mejorar el código existente, hacerlo mas mantenible y acorde a los principios y estilos definidos para el proyecto. En algunos casos el proceso inluye la corrección de los problemas detectas con la participación del autor, el revisor y el resto del equipo. 

## Principios del code review

+ Completo
+ Obligatorio
+ Periódico 
+ Trazable
+ Automatizado
+ Medible
+ Reproducible
+ Integrado
+ Público
+ Impersonal
+ Aislado
+ Interno / Externo
+ Profundo

### Completo 
Todo el código ya sea código en produccion o en desarrollo debe ser revisado, esto puede lograrse estableciendo un requerimiento de revisón y aprobación en cada Pull Request, o bien realizando revisiones periodicas de todo el código. Cada parte del codigo debe revisarse, frontend, backend, css, pruebas automatizadas, scripts de sql, documentación e incluso los casos de prueba. 

### Obligatorio
Todo el código debe ser revisado, ya sea el que incorporan lo arquitectos y lideres, bugfixes, hotfixes. Todos deben saber que el código va a ser revisado antes de ser integrado en el repositorio. 

### Periodico
La revisión debe ser periodica y veces fuera del contexto de los Pull Request ya que a veces una porción de código puede tener sentido en el marco de un Pull Request pero representa una repetición del codigo o una desviacion del estandard en el resto del desarrollo. También puede pasar que las reglas del propio code review hayan cambiado y una parte del proyecto este por fuera de estas reglas por haber sido evaluado en otro momento. 

### Trazable
Deberiamos poder trazar cada porción de codigo con quien fue el autor y el/los revisores que lo aprobaron. 

### Automatizado 

Deberiamos poder detectar y/o corregir todos los errores de estilos con herrmientas automatizadas (linters, warnings de compiladores, spellcheckers, stylecheckers) para centrar los esfuerzos humanos del review en los problemas en algoritmos complejidad, nombres etc. 

### Reproducible

Idealmente dos revisores  diferentes con los mismos principios de diseño y estilo definidos deberian producir los mismos comentarios para el mismo código. Deberiamos tratar de excluir cosas opinables o sujeto de debate entre miembros del equipo. En el caso de que surja algun debate en una revisión debe estar incluido en el proceso quien va a juzgar cual es la mejor manera de hacer algo y esta decision debe incluirse en la documentación y estilos del proceso de revisión de código. 

### Publico
Todos los miembros del equipo pueden ver que código está siendo revisado y cualquier persona puede agragar un comentario a cualquier porcion de codigo de un Pull request. Debemoa evitar establecer una jerarquia que impida opinar sobre el codigo y proponer mejoras. 

### Impersonal
La revisión del código on se hace contra el autor del código, es contra el codigo mismo y se hace con el espiritu de mejorarlo. Debemos evitar adjetivar sobre el codigo y distinguir entre loa gustos personales y los estandares estblecidos.

### Aislado
Cuanod hacemos revisión de código debemos intentar abstraernos de las condiciones concretas con que se desarrollo esa porcion de codigo (deadlines, plazos, falta de presupuesto, hofixes, mala calidad del resto del código, etc). Las mejoras que se propongan pueden realizarse en ese momento o cuando se cuente con mas o mejores recursos para el desarrollo. 

### Interno / Externo
La revisón de codigo debe ser realizada diariamente por los propios miembros del equipo y es una buena practica tener revisiones de codigo externas de otros desarrolladores en diferentes momentos del proyecto. Esto puede ayudar a identificar partes del código dificiles de entender, practicas no estandard, o desviaciones de los estandares de la comunidad o de la organización. 
