##Herencia funcional en JavaScript

Si JavaScript no tiene clases, ¿como se implementa la herencia? es tal vez una de las preguntas que todo desarrollador se ha planteado, en este post intentaremos terminar de dar respuesta esto.

![](https://medium2.global.ssl.fastly.net/max/2048/1*8TxkZzlVLG1uw-xOmwNtAQ.png)**

En [JavaScript: The Good Parts](http://shop.oreilly.com/product/9780596517748.do) escrito por [Douglas Crockford](https://en.wikipedia.org/wiki/Douglas_Crockford), habla sobre *factory functions*, las cuales son la base para realizar herencia funcional (no confundir con programación funcional)

Recuerda que existen tres maneras de realizar [herencia en JavaScript](https://medium.com/@yeion7/entendiendo-la-herencia-en-javascript-288a578edd5b):

* **[Delegación](https://medium.com/@yeion7/entendiendo-la-delegaci%C3%B3n-en-javascript-8d99e3bc3826#.82z6zlqdf)**: Delegar comportamientos a objetos vinculados vía *[[Prototype]]*

* **[Composición](https://medium.com/@yeion7/entendiendo-la-composici%C3%B3n-en-javascript-ac7f0c384b8c#.9f6kfzavr)**: Componer objetos basados en ejemplos o prototipos, vía *Object.assign()*

* **Funcional**: Componer objetos mediante funciones.

Hoy hablaremos de la tercera, pero vayamos paso a paso.

###Herencia funcional

Como ya dije, el promotor de esta es Douglas Crockford, quien en gran parte de sus conferencias nos habla de los peligros de la herencia clásica y el uso de *this* en JS.

Él promueve un sistema de objetos libre de clases, planteando el uso de *factory functions*, estas básicamente son funciones que utilizan varios conceptos, como:

* Poder retornar objetos en una [función](https://medium.com/@yeion7/funciones-de-alto-orden-en-javascript-42d04769d9b5).

* Poder crear [objetos literales](https://medium.com/@yeion7/entendiendo-los-objetos-en-javascript-3a6d3a0695e5).

* La [naturaleza dinámica](https://medium.com/@yeion7/propiedades-internas-en-javascript-717057026516) de los objetos.

* [Closures](https://medium.com/@yeion7/entendiendo-closures-en-javascript-8fb9a284964e).

Veamos esto en un ejemplo

```js
const humano = function(name) {
    return {
      nombre: name,
      genero: '',
      ciudad: 'Bogota',
      decirGenero() {
        console.log(this.nombre + ' mi genero es ' + this.genero )
      },
      decirCiudad() {
        console.log(this.nombre + ' vivo en ' + this.ciudad)
      }

    };
}

const hombre = function (name) {
    const that = humano(name);

    return Object.assign({},
                         that,
                         {genero: 'Masculino'}
                        )
}

const mujer = function (name) {
    const that = humano(name);

    return Object.assign({},
                         that,
                         {genero: 'Masculino'}
                        )
}
const david = hombre('David');
const jane = mujer('Jane');

david.decirGenero();
david.decirCiudad();

jane.decirGenero();
jane.decirCiudad();
```

Como vemos, simplemente tenemos funciones que retornan objetos, los cuales pueden ser genéricos (*humano*) o pueden ser más específicos (*mujer* y/o *hombre*), cada función nos va a retornar un objeto independiente.

Pero el poder de las *factory functions* no queda en esto, con ellas y utilizando el concepto de closures podemos tener propiedades privadas.

```js
const contador = function(salto) {
  let contador = 0;

  return {
    siguiente() {
      contador += salto;
    },
    ver() {
      console.log(contador)
    },
    reset() {
      contador = 0;
    }
  }
}

const contadorDos = contador(2);


contadorDos.siguiente()
contadorDos.ver() // 2
contadorDos.siguiente()
contadorDos.ver() // 4
contadorDos.reset()
contadorDos.siguiente()
contadorDos.ver() // 2
```

Como vemos, tenemos una propiedad (*contador*), la cual no puede ser accedida desde los objetos creados por esta *factory*, pero los métodos en este si pueden hacer gracias a closure.

Como vemos es bastante simple, por eso se utiliza en gran número de librerías dentro de JavaScript, por ejemplo en

* [Express](http://expressjs.com/es/) al crear una aplicación, retorna un objeto

* [Jquery](http://jquery.com), al usar $(Selector), retorna un objeto

* etc

###Ventajas

* **Simplicidad**: Solo se requieren unos cuantos pasos para conseguir realizar herencia.

* **Libre de [this](https://medium.com/@yeion7/entendiendo-this-javascript-cba60c8cec8c)**: Podemos dejar de preocuparnos de *this* o como en los ejemplos su uso es bastante sencillo.

* **Encapsulación**: Objetos pueden tener miembros privados

* **Cada objeto es único:** Cada vez que se llama la función crea un objeto, de esta manera podemos controlar la mutación.

Para mi la principal ventaja de la herencia funcional es la simplicidad, ya que esta es la que principalmente afecta todo nuestro proyecto, te recomiendo leer este [paper](http://curtclifton.net/papers/MoseleyMarks06a.pdf) sobre la complejidad a los proyectos.

###Desventajas

Existen dos grandes “desventajas” que toda persona nombra cuando se trata de herencia funcional o factory functions.

1. *El rendimiento creando objetos es menor.*

Esto es cierto, pero veamos que tanto, si realizamos [esta prueba](https://gist.github.com/yeion7/b4613ba0a72d4a8017cae372cce176d2) donde medimos cuánto demora en crearse un objeto con objetos literales, factory functions y constructores, obtenemos:

```
Constructor: 0.00002ms

Factory: 0.00004ms

Literal: 0.00001ms
```

Como vemos la velocidad de creación de un objeto es mínima y la diferencia para que llegue a ser significativa seria al crear al menos de diez mil objetos (aun asi sera solo de 2ms)

Otra consideración es que al usar una función constructora, aunque tiene mejor rendimiento, se debe usar muchas veces [*bind](https://medium.com/@yeion7/entendiendo-this-javascript-cba60c8cec8c)* para tener el comportamiento deseado de *this*, esto también afecta el rendimiento.

> Nota: Estos valores pueden variar dependiendo del engine que uses y varios factores, aun así si decides realizar microbenchmarks como este, te recomiendo ver antes [esta conferencia](https://www.youtube.com/watch?v=g0ek4vV7nEA).

2. *El consumo de memoria es mayor*

Esto también es cierto ya que cada objeto creado con una *factory function* se creará y guardará en memoria como un objeto independiente.

Pero con el valor actual de memoria, ¿es justificable esta desventaja?

###Herencia funcional vs herencia clásica

Una consideración importante a mi parecer es la simplicidad y la flexibilidad, tomando solo esos dos factores en cuenta considero que las factory functions son una mejor opción.

Pero si se desea priorizar el rendimiento (micro optimizando) la mejor opción sería usar funciones constructoras (clases), esta [respuesta en quora](https://www.quora.com/When-should-I-use-JavaScript-prototypes-in-real-world-applications/answer/Mattias-Petter-Johansson?srid=IviF) te explicara mejor esto.

###Conclusión

JavaScript nos provee de un sistema de herencia increíble, con el cual podemos crear sistemas grandes pero a su vez flexibles y mantenibles.

En este punto te preguntarás ¿eso es todo?, yo también me hice esa pregunta, la respuesta corta es sí y esto es lo increible de JavaScript, ser muy simple, pero a su vez poderoso.

Como vimos los tres tipos de herencia son bastante simples, pero se requiere practicar y saber como usarlos, en próximos post, traeré ejemplos sobre su implementación que nos permitan explorar estos más a fondo, por ahora te recomiendo leer este [post](http://www.nauzethdez.com/javascript-5-herencia-o-composicion/) es muy bueno y te mostrará la flexibilidad de la herencia en JS, también buscar repositorios de librerías y leer el código es una practica que te ayudará a ser mejor desarrollador.
