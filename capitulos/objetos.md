
#Entendiendo los Objetos en JavaScript

##Los objetos son, una de las características menos entendidas en JavaScript, dado que su implementación tiene algunas diferencias…

##Entendiendo los Objetos en JavaScript

Los objetos son, una de las características menos entendidas en JavaScript, dado que su implementación tiene algunas diferencias importantes con muchos lenguajes de programación más tradicionales.

Vayamos paso a paso, intentando entenderlos.

![](https://medium2.global.ssl.fastly.net/max/2048/1*RiM5xNcBXEd_oszdsokNNQ.png)**

En palabras simples:
> #Los objetos son una colección de propiedades

Para construir objetos podemos hacerlo de dos maneras,

* **Objetos declarativos o literales**: podemos crear objetos sin necesidad de un constructor o instanciar una clase, para esto solo declaramos el objeto y sus propiedades.

<iframe src="https://medium.com/media/e74f68358a06c5efe039a38e9ae54f6e" frameborder=0></iframe>

* **Objetos construidos: **JavaScript es un lenguaje libre de clases, pero tenemos el keyword *new*, el cual nos permite crear un nuevo objeto, de esta manera podemos utilizar una función que cumpla el rol del constructor.

<iframe src="https://medium.com/media/62acbf25e4d75ff0e31ea51ffe5bde99" frameborder=0></iframe>

###Contenido

JavaScript no almacena el contenido de las propiedades dentro de los objetos, este solo guarda el nombre de las propiedades, con referencias a donde están almacenados los valores.

<iframe src="https://medium.com/media/ea17507b29f3a37adde980084c47139a" frameborder=0></iframe>

###Acceder a propiedades

Para acceder a las propiedades tenemos dos opciones

* notación con .

* notación con []

<iframe src="https://medium.com/media/bedbeffb6b19d1131c596c240d1ad851" frameborder=0></iframe>

###Atributos de las propiedades

Cada una de las propiedades tiene 4 atributos, los cuales son

* value

* configurable

* enumerable

* writable

Para poder ver los atributos usamos *Object.getOwnPropertyDescriptor(target, propiedad)*

<iframe src="https://medium.com/media/510a73bfc48a2a70133a7b010d4b66f7" frameborder=0></iframe>

Sabiendo esto podremos ver nuestro objetos representados como

<iframe src="https://medium.com/media/666c51f9b13cac08dbce5725a1f89494" frameborder=0></iframe>

###Establecer atributos

Para setear nuevas propiedades con atributos personalizados utilizamos *Object.defineProperty(myObj, propiedad, {atributos})*

<iframe src="https://medium.com/media/baefb08bf69d47ba62bc6e2ba2a23653" frameborder=0></iframe>

Veamos cada uno de estos atributos y entendamos mejor a que hacen referencia.

###Writable

Nos permite definir si el valor de una propiedad va a poder ser modificado o no.

<iframe src="https://medium.com/media/64c2b81a0d3a4cc3f4387983b0c414f0" frameborder=0></iframe>

###Configurable

Nos permite definir si los atributos de la propiedad van a poder ser modificados.

<iframe src="https://medium.com/media/1edb26d7d8cd17dfae7c7f0451d75698" frameborder=0></iframe>

###Enumerable

Controla si la propiedad va a ser mostrada cuando se enumeren las propiedades del objeto, como usando for..in

<iframe src="https://medium.com/media/b11c1bf804704f3d310efe4698ab0a23" frameborder=0></iframe>

###Metodos utiles

* *Object.preventExtensions(objeto) *recibe un objeto y retorna un objeto al cual no se pueden agregar nuevas propiedades.

<iframe src="https://medium.com/media/a4bdf1d17f84a529c0da205981a73055" frameborder=0></iframe>

* *Object.seal(objeto) *recibe un objeto y retorna un objeto al cual no se le pueden agregar propiedades, ni configurar las existentes

<iframe src="https://medium.com/media/28e3d74ee6e90b5188f098897d454461" frameborder=0></iframe>

* *Object.freeze(Objeto) *recibe un objeto y retorna uno al cual, no se puede agregar propiedades, modificarlas, o sobrescribir las actuales

<iframe src="https://medium.com/media/3d00a4857bac64c1569329e3cd7619c1" frameborder=0></iframe>

Los objetos en JavaScript son entidades dinámicas que se pueden modificar en cualquier punto, esto aunque es una característica poderosa, no siempre la vamos a querer.

Aplicando los métodos que anteriores vamos a poder llegar a tener objetos inmutables, pero si tuviéramos otros objetos como propiedades, estos no aplican esta inmutabilidad, podríamos crear una función recursiva, que vuelva todas las propiedades de nuestros objetos inmutables o utilizas librerías como [immutable.js](https://facebook.github.io/immutable-js/) .

 

 
