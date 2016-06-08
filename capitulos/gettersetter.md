
#Entendiendo Getters y Setters en JavaScript

##Desde ES2015, tenemos la posibilidad de usar getters y setters para definir propiedades en nuestros objetos. En este post entenderemos como…

##Entendiendo Getters y Setters en JavaScript

Desde ES2015, tenemos la posibilidad de usar getters y setters para definir propiedades en nuestros objetos. En este post entenderemos como funcionan.

![](https://medium2.global.ssl.fastly.net/max/2048/1*DuiZV4VxNqnu3l_TTf5aiA.png)**

Antes de leer este post te recomiendo leer:
> * [Entendiendo this en JavaScript](https://medium.com/@yeion7/entendiendo-this-javascript-cba60c8cec8c)
> * [Entendiendo los tipos en JavaScript](https://medium.com/@yeion7/entendiendo-los-tipos-en-javascript-4c1c718e8e2a#.feskxxu5y)
> * [Entendiendo los objetos en JavaScript](https://medium.com/@yeion7/entendiendo-los-objetos-en-javascript-3a6d3a0695e5)

¿Listo?

En este momento ya deberías conocer el comportamiento y atributos de las propiedades de los objetos en JavaScript.

En este punto cabe aclarar que los objetos tienen tres tipos de propiedades:

* [*Data properties](https://medium.com/@yeion7/entendiendo-los-objetos-en-javascript-3a6d3a0695e5#.xgukdwcl7)*: Las propiedades normales, que contienen datos.

* *Accessor properties*: Propiedades que cambian el comportamiento estándar de [[get]] y [[put]]

* *Internal properties: *propiedades internas del lenguaje, como [[prototype]], [[get]] o [[put]] entre otros.

###Qué son los getters y setters

Una función que obtiene un valor de una propiedad se llama *getter* y una que establece el valor de una propiedad se llama *setter*.

Esta característica a sido implementada en ES2015, pudiendo modificar el funcionamiento normal de establecer u obtener el valor de una propiedad, a estas se les conoce como *accessor properties.*

###Funcionamiento

En ocasiones queremos valores basados en otros valores, para esto los data accessors son bastante útiles.

Para crearlos usamos los keywords *get* y *set*

<iframe src="https://medium.com/media/078b953486d048bf0db98f392688b3bc" frameborder=0></iframe>

Creamos un objeto, con una única propiedad, que tiene un getter y un setter. de esta manera cada vez que establezcamos un valor para *prop *se multiplicará por dos.

Nota: utilice* __prop__ *por convención, pero no implica que es un valor especial, este es un valor normal.

Otra manera de crear un *accessor properties* es de manera explícita usando *Object.defineProperty*

<iframe src="https://medium.com/media/f7d9fe5e912238dadf9b30018f3791cb" frameborder=0></iframe>

La ventaja que tenemos de esta manera, es que podemos establecer los atributos que queremos tenga la propiedad.

###Características

Una *accessor property*, solo tiene los atributos *configurable* y *enumerable, *si vemos sus atributos veremos esto.

    [object Object] {
       configurable: true,
       enumerable: true,
       get: function get() {
         return this.__prop__;
       },
       set: function set(value) {
         this.__prop__ = value * 2;
       }
    }

Esto nos lleva a que el valor no puede ser sobreescrito si no se usa el *setter* de la función (se recomienda definir ambos *setter* y *getter*).

***nota***: Si no se usa *strict mode *y se intenta modificar el valor va a ser un error silencioso.

Otra característica importante, es que, si se establece una propiedad con el mismo nombre en un ámbito superior de la cadena de prototipos, el accessor property, va a ser la propiedad que predomine.

Veamos un último ejemplo

<iframe src="https://medium.com/media/551ec01bb03e4b94907ec13543e5db18" frameborder=0></iframe>

 

 
