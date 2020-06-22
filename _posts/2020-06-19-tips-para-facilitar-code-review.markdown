---
title:  "Tips para facilitar el code review"
date:   2020-06-19 11:30:05 -0300
tags: software bestPractices codeReview
categories: software
toc: true
---
El code review normalmente se hace en el proceso de aprobación de un pull request si estos pull request son demasiado grandes/largos o poco descriptivos puede ser que nadie los quiera revisar. 

Algunos tips/estrategias para facilitar el code review. 

## Mejor prevenir que curar
### :point_up: El tamaño de las historias. 
Tratar de no hacer historias muy grandes una historia muy grande acarrea un pull request muy grande, si atajamos esto a tiempo vamos a mejorar los tiempos de entrega de la historia, el testing y por supuesto el code review.

Esto puede traducirse en un limite de la cantidad de puntos de una historia acordado en el equipo y con el Product Owner, por ejemplo si una historia lleva más de 5 puntos se hace un slicing :scissors: y se la divide. 

### Un mundo ideal, historias sin puntos :1234:
Con un gran grado de madurez :evergreen_tree: de un equipo podemos incluso llegar a un ideal donde no tengamos puntos por historias sino simplemente historias de un tamaño más o menos constante, si una historia es muy grande se divide en dos o tres de estas historias de tamaño constante.

De esta forma atajamos de inicio el problema del tamaño del pull request y facilitamos el review previniendo el problema. 

## Pull requests propiamente dichos

### Buena Descripción
La descripción del PR es la carta de presentación de nuestro PR :notebook:, links, a las historias o bugs involucrados :bug:, una buena descripción, textual, decisiones de arquitectura que se tomaron, los mensajes de commit, todo suma a la hora de dar contexto y motivar a la persona que tiene que leer el código para detectar problemas. 


### Un Screenshot !
Una imagen :tv: vale más que mil palabras, si estamos con un componente visual incluir algunos screenshots en la descripción del pull request puede cambiar mucho a la hora de dar contexto al revisor y a motivarlo a que revise el PR.
En el caso de una API, incluir una muestra del JSON o del Request y Response  de entrada y salida también ayudan mucho a la hora de sumar revisores.  
 
### Que sean parciales
Hacer Pull request parciales, por ejemplo si una historia implica la creación de un componente nuevo, hacer un PR para cada componente y después otra con la integración de ese componente. Si implica una API y su uso en el front, es mejor dividir cada parte y presentarlo en pull requests separados.

### Que sean completos      
La parcialidad de un Pull request debe encerrar a su vez algo completo, por ejemplo se puede mandar una clase pero con su unit test, o bien un componente sin su utilización, o bien una página que le falta una parte o un formulario sin sus validaciones o ir agregando las validaciones por parte. 

En el caso de una API, para un formulario, por un lado el get de los datos a editar, por el otro el post que hace el alta, y por otro lado el manejo de errores y validaciones. 

Si ya tenemos algo que funciona aunque sea parcialmente con sus unit test ya se puede hacer un PR con esa funcionalidad, podemos usar feature toggle para ocultarlo o alguna condición de ambiente (if environment.production ...) 

### Evitar cambios por formateo automático
 Evitar cambios solo por formateo automatico, cuando usamos un formateador automatico evitar cambiar archivos o lineas que no estamos tocando por funcionalidades o porciones del archivo solo por fines esteticos (saltos de linea, espacios, tipos de comillas, etc).
 
 En caso de ser necesario armar un PR solo con los arreglos de formateo y otro con la funcionalidad. Esto aplica a cuando nuestro formateador modifica los imports solo para ordenarlos o bien cuando se cambian espaciados masivamente en un archivo sin tocar demasiado la funcionalidad. En el caso de que la situación lo amerite (no se entiende nad en el archivo por temas de formato) hacerlo pero aclarar en el pr con un comentario del propio autor de esta sitacion para alivianar el trabajo del reviewer. 
 
## Comentarios propios
A veces para aclarar una situación extraña o partes del código que pueden llamar la atención se puede agregar un comentario del propio desarrollador en el PR. Esto es preferible a dejar comentarios justificativos en el codigo fuente a modo de excusa por restricciones que se pueden tener a la hora del desarrollo de una user story. 
 
 Mas info sobre pull requests y code review en el tag code review en este mismo blog

