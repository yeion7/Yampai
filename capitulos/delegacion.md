
#Entendiendo la delegación en JavaScript

##Cuando la mayoría de programadores piensa en programación orientada a objetos (OO), generalmente recuerdan lenguajes como Java o C++ donde…

##Entendiendo la delegación en JavaScript

Cuando la mayoría de programadores piensa en programación orientada a objetos (OO), generalmente recuerdan lenguajes como Java o C++ donde una clase es una plantilla estática para crear objetos, heredando estos atributos y métodos dentro del objeto creado.
> #“Si estás creando funciones constructoras y heredando de ellas, no has aprendido JavaScript” — [Eric Elliott](undefined)

Como vimos [antes](https://medium.com/@yeion7/entendiendo-la-herencia-en-javascript-288a578edd5b), JavaScript no tiene clases, pero tiene un sistema de herencia más **simple, flexible y poderoso.**

![](https://medium2.global.ssl.fastly.net/max/2048/1*oVVMU8NZpvHfMGa2aUyXiA.png)**

La palabra herencia podría llegar a crear confusión, ya que esta hace referencia a que un comportamiento donde se está siendo copiado, lo que no sucede en JavaScript, por esta razón [Kyle Simpson](https://twitter.com/getify?lang=es) autor de [You Don’t Know JS](https://github.com/getify/You-Dont-Know-JS), lo define como OLOO (objetos linkeados a otros objetos, por sus siglas en inglés).

Vamos paso a paso y entendamos el sistema de delegación.

###Cadena de prototipos

Todo objeto tiene una propiedad interna [[Prototype]], esta es un vínculo que hace referencia a otro objeto.
> #*[[Prototype]] crea una referencia a otro objeto, la mayoría de los objetos cuentan con una cadena de prototipo a otro objeto. —[ Propiedades internas](https://medium.com/@yeion7/propiedades-internas-en-javascript-717057026516#.em4cy0d6o)*

Este mecanismo es utilizado cuando se hace referencia a un propiedad de un objeto y no es encontrada en este, es ahí cuando el método [[get]], continua buscando en el objeto vinculado via [[Prototype]], a esta serie de vínculos entre objetos se le conoce **cadena de prototipos.**

###Object.prototype

La parte superior de la cadena de prototipos es *Object.prototype*, gracias a este objeto tenemos métodos comunes en todos los objetos como:

* toString()

* valueOf()

* hasOwnProperty( .. )

* isPrototypeOf( .. )
> Cuando creamos un objeto literal automáticamente es vinculado a Object.prototype

###Object.create( .. )

Para controlar este vínculo podemos crear objetos con [*Object.create( .. )](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Object/create)*, quien recibe un primer argumento, que es el objeto al cual se vincula por medio de [[Prototype]] y un segundo argumento, con las nuevas propiedades nuevas.

Veamos un ejemplo.

<iframe src="https://medium.com/media/c97363a8c8c946fa3be17ea9e0a98130" frameborder=0></iframe>

Una representación de gráfica de esto sería.

![](https://medium2.global.ssl.fastly.net/max/2000/1*iVmW3UVprFJ3V7WJ6Kz1zQ.png)**
> Object.create(null) crea un objeto que tiene un vínculo vacío, así que el objeto no delega nada, no tiene una cadena de prototipos

###Delegando comportamientos

Ya sabemos podemos manejar el vínculo entre los objetos, esta es la clave de la delegación en JavaScript, de esta manera solo debemos preocuparnos de objetos y las propiedades delegadas entre ellos.

<iframe src="https://medium.com/media/03d94c30fff3338562f8d64880d5c64c" frameborder=0></iframe>

Como vemos podemos crear dos objetos y vincularlos al objeto que usamos como prototipo, y su comportamiento va a ser independiente.

###Mutación

Algo de lo que debemos tener cuidado es de la **mutación**, ya que los objetos en JavaScript son dinámicos.

Si una propiedad se cambia en un objeto se cambia en todos, claro este comportamiento es esperado si sabemos como funciona los [tipos en JavaScript](https://medium.com/@yeion7/entendiendo-los-tipos-en-javascript-4c1c718e8e2a#.k6s9jvnmp).

<iframe src="https://medium.com/media/ab6c89cbd4c174e9ab21f2fc1fe88c02" frameborder=0></iframe>

En el siguiente post veremos **composición**, lo cual nos ayudará a controlar esto y tener un sistema de herencia mucho más poderoso.

Me gustaría presentarles un ejemplo algo más complejo el cual tomó de [You Don’t Know JS](https://github.com/getify/You-Dont-Know-JS), en su libro dedicado a [objetos](https://github.com/getify/You-Dont-Know-JS/blob/master/this%20&%20object%20prototypes/ch6.md).

En este ejemplo tenemos dos objetos controladores, que manejan el formulario de login y la autentificación con el servidor.

**Nota**: Antes de leer el ejemplo te recomiendo [entender como funciona *this](https://medium.com/@yeion7/entendiendo-this-javascript-cba60c8cec8c)*.

<iframe src="https://medium.com/media/1ccc63ee720a7082cc95d224622bb691" frameborder=0></iframe>

<iframe src="https://medium.com/media/015025b7dfc992a17a3023ac3256c683" frameborder=0></iframe>

Con delegación de comportamiento *AuthController* y *LoginController* son solo objetos, solo debemos preocuparnos de delegar comportamientos.

###Conclusión

Utilizar delegación de comportamientos puede llevar a arquitecturas de código más simples.

En este solo debemos pensar en objetos, los cuales delegan comportamientos a otros objetos, lo que lleva a no tener estructuras jerárquicas rígidas.
> #“Hay dos clases de programadores JS, los que aprendimos con JS y los que aprendieron con otro lenguaje y tratan de usar JS como ese lenguaje” — [Sergio Xalambrí](undefined)

Tal vez al principio después de haber utilizado durante mucho tiempo constructores, jerarquías, poliformismos, etc. entender como funciona el patrón de delegación requiere un poco de costumbre, pero esta es mucho más fácil de entender que la herencia clásica.

 

 
