---
title:  "Guia para unit test "
date:   2020-08-12 16:30:05 -0300
tags: software bestPractices unitTest
categories: software
toc: true
author: Walter Casella
---

En este articulo se plantean una serie de tips, metas y guidelines que buscan encausar la práctica de unit testing a partir de una metodología a seguir.

Realizar unit tests es una forma de documentar el funcionamiento esperado de un sistema. Un unit test bien escrito especifica qué se espera que haga una unidad o componente funcional del sistema en un escenario determinado y en qué estado debe quedar el mismo luego de su evaluación.

# Glosario
- AUT: application under test.
- SUT: system under test.
- API: application programming interface.
- Mocks: objetos pre-programados con expectativas que constituyen una especificación de las llamadas que esperan recibir.
- Stubs: proveen respuestas enlatadas a llamadas realizadas durante el test, normalmente no saben responder a nada para lo que no se los haya programado en el contexto del test.
- Test Module: módulo o clase que contiene test methods para testear cierta funcionalidad.
- Test Method: método que contiene el código de un test case.
- Test Case: escenario o caso de test particular.

# Tips para evitar malos unit tests
Algunos desarrolladores toman muy en serio el lema "don't repeat yourself" (DRY). Estamos de acuerdo en que no repetir código es una virtud en la mayoría de los casos, pero el código escrito en un unit test es una excepción: la astucia en un test oscurece la intención del mismo y hace que una falla subsecuente sea mucho más difícil de diagnosticar.

Otros desarrolladores quieren evitar escribir ambos, tests y documentación: intentan escribir casos de test que realizan el trabajo de tests reales, mientras que al mismo tiempo intentan hacer documentos "legibles".

La mayoría de las cuestiones que tienen que ver con el primer motivo son resueltas satisfactoriamente más adelante en esta documentación: rechazando compartir código entre test modules logramos que la mayoría de las tentaciones a ser astuto desaparezcan. Donde la tentación permanezca, la cura es mirar un test individual y responder a las siguientes preguntas:
- ¿Está la intención del test claramente explicada por el nombre del test case?
- ¿El test sigue la forma "canónica" de un unit test? Por ejemplo:
  - Configura las pre-condiciones para el método que está siendo testeado (arrange).
  - Invoca el método exactamente una vez, pasándole los valores establecidos en el primer paso (act).
  - Realiza las afirmaciones sobre el valor de retorno y/o sobre cualquier otro efecto secundario (assert).
  - No hace absolutamente nada más.

Corregir los tests que fallan por el famoso "don't repeat yourself" usualmente es directo:
- Reemplazar cualquier configuración "genérica" de código con código por test case. El caso clásico aquí es código en un método decorado con el atributo `[ClassInitialize]` o `[TestFixtureSetUp]` (según el test framework) que almacena valores en la propia instancia de la clase que representa el test case: ese tipo de código siempre es posible de ser refactorizado usando métodos helpers que retornen los test objects configurados apropiadamente en función de cada test.
- Si el método bajo test es llamado más de una vez, clonar (y renombrar apropiadamente) el método del test case, removiendo cualquier setup / assertion redundantes, hasta que cada test case lo llame exactamente una vez.

Reescribir tests que conforman con este patrón tiene un número de beneficios:
- Cada test case individual especifica exactamente un path de código a través del método que está siendo testeado, lo que implica que alcanzar "100% coverage" significa que uno realmente ha testeado todo.
- El conjunto de test cases para el método que se está testeado define el contrato muy claramente: cualquier ambigüedad puede ser resuelta agregando uno o más tests adicionales.
- Cualquier test que falle va a ser más fácil de diagnosticar, porque la combinación de su nombre, sus pre-condiciones, y sus resultados esperados van a estar claramente enfocados.

# Metas
Las metas del tipo de testing descrito en este articulo son la simplicidad, el bajo o ningún acoplamiento, y la velocidad:
- Los tests deben ser tan simples como sea posible, mientras ejecuten completamente la AUT.
- Los tests deben correr tan rápido como sea posible, para alentar su ejecución frecuentemente.
- Los tests deben evitar el acoplamiento con otros tests, o con partes de la AUT sobre las que no son responsables de testear.
- Los tests deben poder ser programados para su automática ejecución con la frecuencia que se considere necesaria (típicamente en cada CI).

Los desarrolladores escriben este tipo de tests para verificar que la AUT está cumpliendo con los contratos que los analistas y ellos mismos especifican. Mientras que un ejemplo de este tipo de test case puede ser ilustrativo del contrato que testea, estos test cases no ocupan el lugar de la documentación de la API ni de la documentación narrativa. Menos aún están pensados como documentación para el usuario final.

# Guidelines

## Mantenga los unit tests pequeños y rápidos
Lo ideal sería que todo el conjunto de unit tests se ejecute antes de cada integración de código. Mantener los tests rápidos reduce los tiempos de desarrollo.

## Los unit tests deben ser totalmente automatizados y no interactivos
El conjunto de tests normalmente es ejecutado de forma regular y debe ser totalmente automatizado para ser útil. Si los resultados requieren inspección manual, los tests no son unit tests adecuados.

## Haga los unit tests fáciles de ejecutar
Configure el entorno de desarrollo de manera que tests simples y conjuntos de tests puedan ser ejecutados por un simple comando o por un clic de un botón.

## Mida los tests
Aplique análisis de cobertura a los tests ejecutados para que sea posible leer exactamente la cobertura ejecutada e investigar cuáles partes del código se ejecutaron y cuáles no.

## Corrija los tests fallidos inmediatamente
Cada desarrollador debe ser responsable de asegurarse que un nuevo test se ejecuta satisfactoriamente hasta su commit, y que todos los tests existentes se ejecutan satisfactoriamente hasta la integración del código.

Si un test falla como parte de una ejecución regular de tests, el team completo debe dejar lo que está haciendo en ese momento y asegurarse de que el problema sea resuelto.

## Mantenga el testing al nivel de unidad
El unit testing trata acerca de testear clases. Debe haber una clase de test por cada clase ordinaria y el comportamiento de la clase debe ser testeado en aislamiento. Evite la tentación de testear un workflow completo utilizando un framework de unit testing, dado que esos tests son lentos y difíciles de mantener. El testing de un workflow tiene su lugar, pero no en el unit testing y debe ser configurado y ejecutado de forma independiente.

## Comience de forma simple
Un test simple es infinitamente mejor que ningún test en absoluto. Una simple clase de test establecerá el test framework, verificará la presencia y funcionamiento tanto del entorno de build, del de unit testing, como del entorno de ejecución y de la herramienta de análisis de cobertura, y probará que la clase a testear es parte de un assembly y puede ser accedida.

El _Hello, world!_ de los unit tests podría ser algo así:
```
[Fact]
public void Puedo_instanciar_Foo()
{
    Foo foo = new Foo();
    Assert.IsNotNull(foo);
}
```

## Mantenga los tests independientes
Para garantizar la solidez del testing, simplificar el mantenimiento y posibilitar la paralelización de su ejecución, los tests nunca deben depender de otros tests ni tampoco deben depender del orden en que son ejecutados.

## Mantenga los tests de un proyecto en otro de igual nombre pero con el sufijo ".Tests.Unit"
Para cada proyecto a testear de la solución debe existir otro proyecto homónimo cuyo nombre tenga el sufijo `.Tests.Unit` (esto es para diferenciarlos de los proyectos que contienen integration tests, cuyos nombres finalizan con el sufijo `.Tests.Integration`).

Si la clase a testear es `Foo`, la clase de test debe llamarse `FooTests` (no `TestFoo`, ni `FooTest`, ni `TestsFoo`).

## Organice los diversos tests sobre un método de una clase dentro de una inner class
Organice los diversos tests que se escriban para probar distintos escenarios sobre un método particular de una clase dentro de una inner class que los agrupe:
```
public class FooTests
{
    public class ElMetodo_Saludar : FooTests
    {
        [Fact]
        public void Dice_hola_si_establezco_idioma_espanol()
        {
            ...
        }

        [Fact]
        public void Dice_hello_si_establezco_idioma_ingles()
        {
            ...
        }
    }
}
```
Este tipo de agrupamiento / organización dará mayor claridad y expresividad a los tests.

## Nombre los tests de forma apropiada
Asegúrese de que cada test method prueba una característica distintiva de la clase que está siendo testeada y nombre los test methods en consecuencia. La convención es que el nombre del método deje claros el estado y comportamiento esperados del objeto testeado, separando las palabras con underscore (no pascal case), por ejemplo: `Debe_incrementar_balance_cuando_se_hace_deposito()`.

## Testee la API pública
La práctica de unit testing puede ser definida como testear clases a través de la API pública. Algunas herramientas de testing hacen posible testear el contenido privado de una clase, pero esto debe ser evitado ya que hace el test más detallado y mucho más difícil de mantener. Si existe contenido privado que parece necesitar un testing explícito, en su lugar, considere refactorizarlo en métodos públicos dentro de clases de tipo utility, helper, o (mejor aún) que representen el dominio del problema que se está abordando. Pero haga esto para mejorar el diseño general, no para agregar testing.

## Piense black-box
Actúe como un consumidor de clases de librerías de terceros y testee si la clase cumple con sus requerimientos, y trate de destrozarla.

## Piense white-box
Después de todo, el desarrollador del test también escribió la clase que está siendo testeada, y un esfuerzo adicional debe ser puesto en testear la lógica más compleja.

## Testee también los casos triviales
A veces se recomienda que todos los casos no triviales sean testeados y que los métodos triviales pueden ser omitidos. Sin embargo, existen varias razones sobre por qué los casos triviales también deben ser testeados:
- "Trivial" es difícil de definir. Puede significar diferentes cosas para diferentes personas.
- Desde una perspectiva black-box no existe forma de saber qué parte del código es trivial.
- Los casos triviales pueden contener errores también, muchas veces como resultado de una operación de copy-paste.

Por lo tanto, la recomendación es testear todo. Los casos triviales son fáciles de testear después de todo :smile:.

## Céntrese en la cobertura de ejecución primero
Diferencie entre cobertura de ejecución y cobertura de test real. La meta inicial de un test debe ser asegurar alta cobertura de ejecución. Esto certificará que el código realmente es ejecutado sobre algunos parámetros de entrada. Cuando esto esté en su lugar, la cobertura de test debe ser mejorada. Tenga en cuenta que la cobertura de test real no pude ser medida fácilmente (y de todas maneras siempre está cerca del 0%).

Considere el siguiente método público:
```
public void SetLength(double length)
{
	...
}
```
Invocando SetLength(1.0) es posible obtener cobertura de ejecución del 100%. Para lograr 100% de cobertura de test real este método debe ser llamado para cada valor double posible y el comportamiento correcto debe ser verificado para todos ellos. Sin duda, una tarea imposible.

## Cubra los casos límite
Asegúrese de que los casos de parámetros límite son cubiertos. Para números testee negativos, cero, positivos, mínimo, máximo, NaN, etc. Para strings testee la cadena vacía (string.Empty), una cadena de un sólo carácter, una cadena no ASCII, cadenas de muchos MB, etc. Para colecciones testee vacío, uno, primero, último, etc. Para fechas (DateTime), testee 1 de Enero, 29 de Febrero, 31 de Diciembre, etc. La clase que esté siendo testeada sugerirá los casos límite en cada caso específico. El punto es asegurarse de que el mayor número posible de ellos sean testeados adecuadamente, ya que estos casos son los principales candidatos para los errores.

## Proporcione un generador aleatorio (random)
Cuando los casos límite están cubiertos, una manera simple de mejorar la cobertura de test es generar parámetros aleatorios para que se puedan ejecutar con diferentes entradas cada vez.

Para lograr esto, provea una clase simple de tipo helper / utility que genere valores aleatorios para los tipos de datos base como `double`, `int`, `string`, `DateTime`, etc. El generador debe producir valores del dominio completo de cada tipo.

## Testee cada aspecto solo una vez
Cuando uno está en _modo testing_ a veces es tentador realizar el assert de todo en cada test. Esto debe ser evitado ya que hace que el mantenimiento se dificulte. Testee exactamente el aspecto indicado por el nombre del test method.

Así como para el código ordinario, mantener la cantidad de código de test tan baja como sea posible es una meta.

## Utilice asserts explícitos
Preferir siempre `Assert.Equal(a, b)` en vez de `Assert.True(a == b)` (y construcciones por el estilo) ya que la primera construcción dará mucha más información acerca de qué es lo que está mal exactamente si el test falla. Esto es particularmente importante en combinación con los parámetros con valores aleatorios, como se describió anteriormente, cuando los valores de entrada no se conocen de antemano.

## Proporcione tests negativos
Los tests negativos hacen un mal uso del código intencionalmente y verifican robustez y manejo de errores adecuado.

Considere este método que arroja una excepción si es llamado con un parámetro negativo:
```
/// <exception cref="ArgumentOutOfRangeException"></exception>
public void SetLength(double length)
```
El testing del correcto comportamiento para este caso particular puede hacerse de la siguiente manera:
```
[Fact]
public void No_puedo_establecer_una_longitud_negativa()
{
    Assert.Throws<ArgumentOutOfRangeException>(() => sut.SetLength(-1.0));
}
```

## Diseñe el código pensando en el testing
Escribir y mantener unit tests es costoso, y minimizar la API pública y reducir la complejidad ciclomática en el código son formas de reducir este costo y de hacer que tenga alta cobertura, sea más rápido de escribir y de mantener.

Algunas sugerencias:
- Haga que los miembros de una clase sean inmutables siempre que sea posible, estableciendo su estado al momento de su construcción. Esto reduce la necesidad de setters en las properties.
- Restrinja el uso de herencia excesiva y de métodos públicos virtuales.
- Reduzca la API pública mediante la utilización del scope internal.
- Evite ramificaciones innecesarias.
- Mantenga el menor código posible en las ramificaciones.
- Haga uso intensivo de excepciones y de assertions para validar argumentos en las APIs pública y privada respectivamente.

## No se conecte a recursos externos predefinidos
Los unit tests deben ser escritos sin el conocimiento explícito del contexto y el entorno en que se ejecutan para que puedan ser ejecutados en cualquier lugar y en cualquier momento. Con el fin de proveer los recursos requeridos por un test, éstos deben ser suministrados por el test mismo.

Considere, por ejemplo, una clase para parsear archivos de cierto tipo. En vez de escoger un archivo de ejemplo de una ubicación predefinida, ponga el contenido del archivo dentro del test, escríbalo en un archivo temporal en el proceso de `[TestInitialize]` y elimínelo en el proceso de `[TestCleanup]` (según el test framework utilizado).

## Conozca el costo del testing
No escribir unit tests es costoso, pero escribir unit tests también lo es. Existe un balance entre los dos, y en términos de cobertura de ejecución el estándar típico de la industria está alrededor del 80%.

Las áreas típicas donde es difícil obtener una cobertura de ejecución completa son en el manejo de errores y excepciones que tienen que ver con recursos externos. Simular un colapso en la base de datos en medio de una transacción es posible, pero podría resultar demasiado costoso en comparación con code reviews exhaustivas, que sería un enfoque alternativo.

## Priorice el testing
El unit testing es un proceso típico de abajo hacia arriba, y si no hay suficientes recursos para testear todas las partes de un sistema la prioridad debe ser puesta en los niveles más bajos primero.

## Escriba tests para reproducir bugs
Cuando se reporte un bug, escriba un test para reproducir el bug (un test que fallará) y utilice ese test como un criterio de éxito cuando corrija el código.

## Conozca las limitaciones
¡Los unit tests nunca pueden demostrar la exactitud del código!

Un test que falla puede indicar que el código contiene errores, pero un test exitoso no prueba nada en absoluto.

La aplicación más útil de los unit tests es la verificación y documentación de los requerimientos a bajo nivel, y el testing de regresión: verificar que el código que no debería variar funcionalmente permanezca estable durante su evolución y refactorización.

Consecuentemente, los unit tests no pueden sustituir un diseño inicial adecuado y un proceso de desarrollo sano. Los unit tests deben utilizarse como un valioso complemento a las metodologías de desarrollo establecidas.


# Bibliografía & Referencias

##  Bibliografía
Muchas de las definiciones utilizadas en el presente documento están basadas en la siguiente bibliografía:
Roy Osherove - [The Art of Unit Testing: With Examples in .net](https://www.amazon.com/gp/product/1933988274)

## Referencias
+ [Una breve descripción de black-box y white-box testing](http://www.faqs.org/faqs/software-eng/testing-faq/section-13.html)
+ [Argumentos para no conectarse a recursos externos](http://www.artima.com/weblogs/viewpost.jsp?thread=126923)
+ [Diferencias entre mocks, stubs, fakes y dummies](http://martinfowler.com/articles/mocksArentStubs.html)
+ [Estructurando unit tests](http://haacked.com/archive/2012/01/02/structuring-unit-tests.aspx)
