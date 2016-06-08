
#Entendiendo scopes de variables en JavaScript

##El scope de una variable hace referencia al lugar donde va a vivir esta, o podrá ser accesible, en JavaScript tenemos varias opciones…

##Entendiendo scopes de variables en JavaScript

![](https://medium2.global.ssl.fastly.net/max/2048/1*FNUEMnXAS0CCE_ELCgn0-Q.png)**

El scope de una variable hace referencia al lugar donde va a vivir esta, o podrá ser accesible, en JavaScript tenemos varias opciones: global, local y bloque.

Pero vamos paso a paso, y veamos cómo funciona cada una.

###Global Scope

Las variables globales son accesibles en cualquier lugar de nuestro código.

Esto sucede porque cuando creamos una variable global esta es instanciada en el objeto *window*

<iframe src="https://medium.com/media/dc70aa5cce7401527a3d71e85ef53db3" frameborder=0></iframe>

Esto lleva a que podamos llamarlas en cualquier lugar de nuestro código.

<iframe src="https://medium.com/media/24fe20e500b54e9d6b390cd531209f59" frameborder=0></iframe>

Existen dos casos particulares en los que podemos crear variables globales sin darnos cuenta.

1 Cuando queremos definir una variable dentro de una función y no utilizamos *var, let o const* para esto.

<iframe src="https://medium.com/media/e7004b8f5c6fe7495648be5a92309127" frameborder=0></iframe>

2 Cuando pretendemos igualar dos variables definiendolas con un solo keyword

<iframe src="https://medium.com/media/3a61f5ab1f17082fbfe8e35c4b5512f5" frameborder=0></iframe>

Debemos tener cuidado con estos casos, ya que podemos estar creando side-effects al crear variables globales sin darnos cuenta.
> #Utilizar variables globales en nuestro código debería ser evitado, ya que al estar almacenadas en window estas pueden ser sobreescritas y/o llevarnos a tener funciones con side-effects.

###Local Scope

Las variables solo van a vivir en la función donde son creadas, para esto utilizamos el keyword *var*

<iframe src="https://medium.com/media/b676b775fe4ad3179bf8a0ce9e6a4297" frameborder=0></iframe>

La variable local únicamente va a vivir dentro de la función, fuera de ella la variable no está definida.

Pero, en el [articulo anterior](https://medium.com/@yeion7/calculo-lambda-en-javascript-57ea69b427b1), vimos que podemos crear funciones que tomen o retornen una función, la manera que funciona el scope en estas es:

<iframe src="https://medium.com/media/44e9354f2f7104317fd7d1d67612040c" frameborder=0></iframe>

En funciones que retornan funciones, podemos llamar a variables exteriores desde funciones que están anidadas, pero desde las funciones externas no vamos a poder acceder a variables internas de funciones anidadas.

###Block Scope

Desde **ES2015** contamos con los keyword *let* y *const *los cuales nos permite tener un scope de bloque, esto quiere decir que las variables solo van a vivir dentro del bloque de código ( **{dentro de llaves es un bloque} **)donde se crean.

<iframe src="https://medium.com/media/14666add35ae6a6b90ceadb4a1894b8d" frameborder=0></iframe>

La variable *i *aun esta en el entorno local de la función, pero como la creamos con *let*, solo va a estar disponible dentro del bloque de código del loop.

En siguientes post veremos más a fondo el funcionamiento de *let* y *const.*

Tener claro donde viven y son accesibles nuestra variables nos va a permitir crear pure functions , lo que es bueno, ya que nos lleva a tener código con menos bugs. Cosa que nos hace feliz a todos.

 

 
