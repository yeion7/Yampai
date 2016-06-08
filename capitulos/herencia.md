##Entendiendo la herencia en JavaScript

La forma como objetos se relacionan entre ellos y se extienden para representar cosas en una aplicación se llama *herencia* y esta es necesaria para crear aplicaciones grandes y complejas.

![](https://medium2.global.ssl.fastly.net/max/2048/1*bztpSB9Rm_rXiVqTU5WKrA.png)**

El sistema de objetos que implementa JavaScript es un sistema basado en prototipos, y libre de clases, entender como funciona te va a permitir comprender uno de los grandes pilares de JavaScript.

Pero vamos paso a paso.

###¿Porque es importante la herencia?

La programación orientada a objetos ganó gran aceptación ya que esta ofrece una perspectiva útil para diseñar programas, buscando hacer portable y reutilizable nuestro código.

Sin embargo no todos los lenguajes tiene la misma perspectiva de como se relacionan los objetos, existiendo diferentes ideas sobre la naturaleza de la programación orientada a objetos.

Pero si esta herencia no es aplicada correctamente, va a llevar a que nuestro software sea difícil de modificar o escalar.

Uno de los lenguaje más famoso del que muchos otros se basaron fue [SmallTalk](https://es.wikipedia.org/wiki/Smalltalk), que implementó herencia basada en clases y jerarquías, de los cuales se han basado muchos lenguajes de programación.

Pero también existen algunas otras ideas, entre ellas, una muy importante fue la propuesta por un lenguaje de programación llamado SELF, el cual propone una herencia basada en prototipos, del cual [Brendan Eich](https://twitter.com/brendaneich) se basó para implementarlo en JavaScript.

<iframe src="https://medium.com/media/77ed1045cca9f82a43cc7abae68bc892" frameborder=0></iframe>

<iframe src="https://medium.com/media/ab5e267c500a846181f8016eb8db7528" frameborder=0></iframe>

Nota: [Acá puedes encontrar los paper de SELF](http://bibliography.selflanguage.org/_static/self-power.pdf), te recomiendo leerlos.

Antes de verlo en JavaScript, me gustaría mostrar algunas ideas que propone SELF

###SELF: el poder de la simplicidad

Uno de los objetivo de SELF fue crear relación más simple entre objetos y para esto como se dice “quitaron toda la grasa” dejando solo objetos, sin necesidad de clases, y para crear una relación entre ellos utilizaron prototipos y clonación.

Dos de las características más importante son:

* *Prototipos*: Combinar herencia y instanciación para proveer una manera más simple y flexible de vincular objetos.

* *Ranuras*: las variables y procedimientos en un constructor simple, que no distingue entre ellas.

También como ya nombre, en SELF, no existen las clases, solo son objetos que sirven como una pieza para construir otros objetos clonándolos, o vincularlos para compartir información.

![](https://medium2.global.ssl.fastly.net/max/2000/1*io3Hk19x39Lz7EG-HhzCqQ.png)**

En contraposición a SmallTalk donde todo es un objeto y se debe instanciar una clase para tener un objeto, en SELF, también todo es un objeto, **pero** estos están vinculados y si se envía un mensaje a un objeto y no se encuentra la propiedad para este, esta seguirá buscando en los objetos vinculados, de esta manera se aplica la herencia.

> #Uno de los aspectos más interesantes es la manera de combinar herencia, prototipos, y creación de objetos, eliminando la necesidad de clases

También es posible, crear nuevos objetos desde prototipos utilizando una operación simple, *clonar*, de esta manera podemos construir objetos desde otros, como piezas de lego.

###¿Cómo se implementa en JavaScript?

JavaScript al basarse en SELF es libre de clases, por lo tanto no se implementa la herencia clásica, dada la implementación del lenguaje se utiliza, **herencia de prototipos** que es más **simple, flexible y poderosa.**

Pero esto ha sido a lo largo de los año una de las cosas menos comprendidas dentro de lenguaje, y se debe a varias cosas.

* Cuando se implementó JavaScript, fue requerida por [Netscape](https://es.wikipedia.org/wiki/Netscape_Navigator) una sintaxis parecida a Java, por esto tenemos en el lenguaje *keywords* como *new* o *instanceof*, lo cual hace creer que se pueden instanciar clases.

* El término herencia hace referencia a copiar, y este término no hace representa la manera como se aplica esto en JavaScript, por esto autores como [Kyle Simpson](https://twitter.com/getify?lang=es) autor de [You Don’t Know JS](https://github.com/getify/You-Dont-Know-JS) hace aclaración que se debería nombrar como OLOO (objetos linkeados a otros objetos, por sus siglas en inglés)

Ya que muchos desarrolladores no entienden este sistema de herencia implementado en JavaScript, han intentando simular o implementar cosas parecidas a herencia clásica, pero todas estas funcionan sobre la herencia de prototipos.

###¿Qué diferencias existen?

**Herencia clásica:** una clase es como un plano, que describe los atributos y métodos de los objetos a ser creados, las clases pueden heredar de otras clases (reutilización de código), crean una relación jerárquica.

En muchos lenguajes esta es la única manera de crear objetos, pero en algunos pocos, los objetos pueden ser creados sin necesidad de instanciar una clase (como en JS), así que el tener que instanciar una “clase”, es en sí un patrón llamado **constructor**.

En JavaScript se implementa este patrón, utilizando una función como constructor, y “instanciando” con el keyword *new*, y se utiliza el método interno [[prototype]] para delegar propiedades, así crear una jerarquía.

Todo esto se implementa sobre la herencia de prototipos pero no tiene el mismo poder y flexibilidad, ya que se cae en todos los problemas de la herencia clásica.

**Herencia de prototipos:** Objetos se vinculan directamente de otros objetos, se pueden vincular a uno o varios objetos.

En JavaScript tenemos tres maneras correctas de implementar esta herencia de prototipos.

*Concatenación*: Se copian propiedades de uno o varios objetos, en un nuevo objeto destino, a esto también se le conoce como *mixins*, y desde *ES2015*, se cuenta con una manera sencilla de hacerlo con *Object.assign()*

*[Delegación](https://medium.com/@yeion7/entendiendo-la-delegaci%C3%B3n-en-javascript-8d99e3bc3826)*: Si se consulta una propiedad en un objeto y no se encuentra, se continúa buscando en el objeto al cual esté vinculado por [[prototype]], hasta llegar a *Object.prototype*, para controlar y determinar este vinculo entre objetos contamos con *Object.create()*

*Funcional*: Toda función puede retornar objetos aprovechándose de los [closures](https://medium.com/@yeion7/entendiendo-closures-en-javascript-8fb9a284964e) para tener propiedades privadas, a esto se le llama factory functions, se pueden extender estos objetos retornados directamente.
