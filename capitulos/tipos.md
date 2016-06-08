##Entendiendo los tipos en JavaScript

Una de las características más particulares de JavaScript, es el comportamiento de los tipos de datos, pero conociendo su comportamiento nos permite entender como se comportan nuestros datos durante la ejecución.

![](https://medium2.global.ssl.fastly.net/max/2048/1*iLobnLhtpv4YBUoRnyvHdg.png)**

###¿Que es un tipo?

Básicamente los tipos definen el comportamiento que van a tener los datos.

> “Un tipo es un conjunto integrado de características intrínsecas que identifican el comportamiento de un valor particular y lo distingue de otros valores, tanto para el engine y el desarrollador”
> [You Don’t Know JS: Types & Grammar](https://github.com/getify/You-Dont-Know-JS/blob/master/types%20&%20grammar/ch1.md)

###¿Cuales tipos existen?

La [especificación del lenguaje](http://www.ecma-international.org/ecma-262/5.1/) define los tipos:

* **string**

* **number**

* **boolean**

* **null**

* **undefined**

* **object**

* **symbol**

Antes de continuar, es preciso decir que en JavaScript, las variables no tienen tipos, Los valores son quienes los tienen. Las variables pueden almacenar cualquier tipo.

> “Las variables en JavaScript no tienen tipos, los valores son quienes tienen tipos”

Estos tipos se dividen en dos:

###Primitivos

**string, number, boolean, null, undefined**

Entendamos el comportamiento de estos.

Cuando definimos un valor primitivo:

```js
let variable = “hola”; //string
```

El nombre de la variable se instancia en su [scope](https://medium.com/@yeion7/entendiendo-scopes-de-variables-en-javascript-661ea382c8bc), y este nombre hace referencia a la ubicación en memoria, donde está almacenado el valor.

![](https://medium2.global.ssl.fastly.net/max/2000/1*ciEN0bQ7HtRCscINzWYPNQ.png)

Ahora, si asignamos esta variable a otra, el valor se copia, a otra posición en memoria, y cada variable apunta a una ubicación distinta.

![](https://medium2.global.ssl.fastly.net/max/2000/1*9i0KzR9Y-mWPsWhfh7G9qw.png)**

Este comportamiento, hace que si nosotros declaramos un valor primitivo dentro de una variable con *const*, será inmutable, ya que este no podrá ser reasignado.

###Por referencia

**object**

Los objetos definen subtipos, los cuales son: **String, Number, Boolean, Object, Function, Array , Date, RegExp, Error**

Cuando definimos un objeto:

```js
let obj = {nombre: ‘yeison’}
```

El nombre de la variable se instancia en su [scope](https://medium.com/@yeion7/entendiendo-scopes-de-variables-en-javascript-661ea382c8bc), y este hace referencia al objeto en memoria, este contiene una lista de sus propiedades, que a su vez hacen referencia a donde están almacenados los valores.

![](https://medium2.global.ssl.fastly.net/max/2000/1*VXfqlxGB3GrMygWHTn6Pow.png)**

Ahora si, asignamos *obj* a otra variable, el objeto al que hace referencia no se va a copiar, lo que va a suceder, es que la nueva variable, es otra referencia al mismo objeto.

```js
let obj2 = obj
```

![](https://medium2.global.ssl.fastly.net/max/2000/1*O2raJ1Nvr4s3VUpCe9AwZw.png)**

Por eso, si cambiamos la propiedad *nombre* de *obj2*, ambas variables apuntar al mismo objeto, se va a cambiar también en *obj*

```js
obj2.nombre = “camilo”;

console.log(obj.nombre) // camilo
```

Este es el comportamiento de los objetos en JavaScript, y funciona igual para objetos anidados dentro de otros objetos

```js
let identify = {
  name: {
    first: "yeison",
  },
  social: {
    twitter: "@yeion7"
  }
};
```

Que seria algo asi

![](https://medium2.global.ssl.fastly.net/max/2000/1*MOFkg-iV89qBVsa6xTxVqg.png)**

y si yo hiciera

```js
let identify2 = identify.name

identify2 = {first: “juan”}

console.log(identify.name.first) // ???
```

*¿Que me mostraria en consola?*

Como vimos no todo en JavaScript es un objeto, pero si todos los valores se relacionan a través de referencias/punteros, tener un entendimiento sólido de como funcionan los diferentes tipos nos va a permitir entender como trabajar con nuestros valores, sin llegar a tener mutaciones inesperadas.
