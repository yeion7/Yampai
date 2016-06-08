
#Entendiendo closures en JavaScript

##Un closure es cuando una función es capaz de recordar y acceder a un lexical scope, incluso cuando la función es ejecutada por fuera del…

##Entendiendo closures en JavaScript
> #Un closure es cuando una función es capaz de recordar y acceder a un lexical scope, incluso cuando la función es ejecutada por fuera del lexical scope.

Sencillo ¿cierto?, bueno tal vez no tanto, pero vamos paso a paso y entendamos esto.

Antes de entender mejor el concepto, deberías conocer:

* [Entendiendo scope de variables en JavaScript](https://medium.com/@yeion7/entendiendo-scopes-de-variables-en-javascript-661ea382c8bc#.2exjvcox7)

* [Calculo lambda en JavaScript](https://medium.com/@yeion7/calculo-lambda-en-javascript-57ea69b427b1#.53g71yl6z)

![](https://medium2.global.ssl.fastly.net/max/2048/1*JFABpWZJ6DjGmJqmv2faug.png)**

Los closures son muy utilizados en JavaScript, solo hay que saber reconocerlos dentro del código y las implicaciones de funcionalidad que este tiene.

Los closures están disponibles gracias a que el lenguaje implementa [lambdas](https://medium.com/@yeion7/calculo-lambda-en-javascript-57ea69b427b1#.53g71yl6z) y [funciones de alto orden](https://medium.com/@yeion7/funciones-de-alto-orden-en-javascript-42d04769d9b5#.a0qllgpfi) y son una consecuencia directa de escribir código usando [lexical scopes](https://medium.com/@yeion7/entendiendo-scopes-de-variables-en-javascript-661ea382c8bc#.nftjjvrnr).

veamos esto en código:

<iframe src="https://medium.com/media/dc3d6f1dc23c67abfa9dd1840a790db6" frameborder=0></iframe>

Se tiene una función, que tiene una variable interna, que utiliza la variable *name *y retorna la definición de la función *sayName.*
> Si llamamos la *función sin paréntesis *estamos pasando el objeto función en sí mismo.
> Si llamamos la *función con paréntesis* pasamos el resultado de su ejecución.
> [Funciones de alto orden en JavaScript](https://medium.com/@yeion7/funciones-de-alto-orden-en-javascript-42d04769d9b5#.olaylmi3g)

Pero al ejecutar la función *say*, cuando se asigna a la variable *sayYeison*, su variable interna, no debería ser borrada por el *Garbage Collector, *ya que no está en uso, ¿no?

Esto no es así, ya que al ejecutar la función, se retorna la definición de la función interna que tiene una referencia a este scope, por este motivo la variable no va desaparecer.
> #*El scope interno todavía está en uso, usado por la función que se retorna*

Lo fundamental para poder entender el concepto de closure, es que contamos con una contexto y una función que hace uso de este, permitiéndonos acceder al scope de tal contexto.

Veamos en otro ejemplo.

<iframe src="https://medium.com/media/07b9c81abf4cfe4ba5bda5837f558efe" frameborder=0></iframe>

Aplicando closures podemos crear funciones utilizando diferentes contextos, esto nos lleva a un patrón muy poderoso que veremos en el siguiente post.

Por último veamos una aplicación práctica de closures, tomado de [JavaScript: The Good Parts](http://shop.oreilly.com/product/9780596517748.do) (página 60).

Vamos a crear una función para calcular el [número Fibonacci](https://es.wikipedia.org/wiki/Sucesi%C3%B3n_de_Fibonacci)

<iframe src="https://medium.com/media/c82539727ea7a9cdc30944c8ca2222a2" frameborder=0></iframe>

Podemos ver en la ejecución, se llamó 453 veces a la función *fibonacci, *así con números más grandes esta cantidad crecerá exponencialmente, intentemos mejorar esto aplicando closures.

<iframe src="https://medium.com/media/ef4f78f14a44fe1ca11b62eac714c289" frameborder=0></iframe>

Utilizando un closure, que nos permita almacenar los resultados en un array, el número de veces que se invoca la función ahora es 29.

Puedes encontrar más referencias a este tema en:

* [You Don’t Know JS: Scope & Closures](https://github.com/getify/You-Dont-Know-JS/blob/master/scope%20&%20closures/ch3.md)

* [Closures en MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Closures)

* [JavaScript: The Good Parts](http://shop.oreilly.com/product/9780596517748.do) por [Douglas Crockford](http://www.crockford.com/) (página 37)

 

 
