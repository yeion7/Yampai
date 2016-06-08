
#Funciones de alto orden en JavaScript

![](https://medium2.global.ssl.fastly.net/max/2048/1*pXM2bSSTXueVqF1UnwHCyA.png)**

Este tema me hace especial ilusión, porque me costó entender el concepto, ya que venía de otros lenguajes de programación donde no se veía. Por eso, si puedo ayudarte a entenderlo sera genial.

Las funciones de alto orden, es un concepto simple pero muy poderoso el cual tienen todos los lenguaje de programación funcionales, es básicamente tratar a las funciones como **ciudadanos de primera clase**, esto significa que las funciones son **objetos** (algunos autores califican a JS como un[ lenguaje OO](https://davidwalsh.name/javascript-objects-deconstruction)).

Si nuestras funciones son objetos, nos da la posibilidad de que sean:

* Almacenadas en variables.

* Pasadas como argumentos.

* Retornadas funciones.

Suena interesante cierto, pero veamos cómo manejar cada caso.

###Ser almacenadas en variables

Partamos de una función.

```js
function porTres(numero) {
  return numero * 3;
}

console.log(porTres(10)); //30
```
No hay nada nuevo, esto se puede hacer en cualquier lenguaje de programación (crear una función, recibir un parámetro y retornar un valor), pero no en todos puedes hacer esto:

```js
let porTres = function(numero) {
  return numero * 3;
}

const multiplicaTres = porTres;

console.log(multiplicaTres(10)); //30
```
Poder almacenar una función en una variable.

Debemos fijarnos en la manera que asignamos a multiplicaTres la función *porTres* sin usar paréntesis, esto es porque:

* Si llamamos la *función sin paréntesis* estamos pasando el objeto función en sí mismo.

* Si llamamos la *función con paréntesis* pasamos el resultado de la ejecución.

[Aqui](https://jsbin.com/fiyefi/edit?js,console) el codigo de los ejemplos.

###Pasarlas como argumentos

Esta es tal vez la característica más utilizada a diario por cada persona que escriba código en JavaScript, ya que nos permite crear c*allbacks.*

Callbacks básicamente son funciones que se ejecutan una vez se hayan terminado de ejecutar una o más funciones, esto nos permite escribir código asincrónico , dado que JavaScript es un lenguaje *Single Threaded* y solo puede manejar un proceso a la vez.

Escribir código asincrónico, nos permite tratar con datos o procesos que podrían tardar tiempo en ser resueltos, sin bloquear el sistema mientras estos se resuelven, para entender cómo funciona esto debemos entender el [event loop](https://www.youtube.com/watch?v=8aGhZQkoFbQ).

Veamos cómo pasar funciones como argumentos en este ejemplo.

```js
/*
Boton dentro de HTML
<button id=”button”>Touch me!</button>
*/
const button = document.getElementById(‘button’);

button.addEventListener(‘click’, function() {
  alert(‘me tocaste!’);
})
```
> Cuando pasando una función como un argumento, esta se va a ejecutar tan pronto suceda el evento, y el sistema no se va a bloquear mientras espera que suceda esto.

En el ejemplo anterior pasamos una función anónima, pero también podríamos pasar como callback una función externa, de esta manera:

```js
button.addEventListener(‘click’, clickAlert)

function clickAlert() {
  alert(‘me tocaste!’);
}
```

Esto nos evitaría caer en un [callback hell](http://callbackhell.com/) y nos permite crear funciones más genéricas, por ejemplo:

```js
<button id=”enviar”>Enviar</button>
<button id=”borrar”>Borrar</button>

const enviar = document.getElementById(‘enviar’);
const borrar = document.getElementById(‘borrar’);

enviar.addEventListener(‘click’, clickAlert);
borrar.addEventListener(‘click’, clickAlert);

function clickAlert() {
  alert(`hiciste click en el boton ${this.id}`);
}
```
[¿Cómo funciona This en JavaScript?](https://medium.com/@yeion7/entendiendo-this-javascript-cba60c8cec8c#.bm3au0dbn)

Manejamos el evento de dos botones, con una sola función, esto hace nuestro código reusable y más limpio. además de darnos la posibilidad de crear [funciones puras](http://www.sitepoint.com/functional-programming-pure-functions/).

[Aquí](https://jsbin.com/yicuda/3/edit?html,js,output) el código de los ejemplos

###Retornar funciones

Por último las funciones de alto orden, nos dan la posibilidad de retornar funciones, esto es una propiedad muy poderosa ya que podemos utilizar funciones que sean templates de otras funciones y al hacer esto podemos utilizar la composición que hará nuestro código más mantenible y escalable.

Para entenderlo mejor, veámoslo en código

<iframe src="https://medium.com/media/b55075fe65104b4f98c7b98450438379" frameborder=0></iframe>

Creamos una función, que retorna otra función, y comprueba el mayor, después “creamos” dos funciones, utilizando nuestra definición de* masGrandeQue, usándola como un template para otra función, para entender un poco más como funciona esto debemos conocer lambdas y closures.

Creemos otro ejemplo algo más útil, que tal si creamos un función que reemplace de cualquier texto una palabra

```js
let reemplace = function(texto) {
  return texto.replace(/mal/ig,”increible”);
};

console.log(reemplace(“JavaScript es un mal lenguaje”));
//"JavaScript es un increible lenguaje"
```
Fácil, ¿cierto?, Que tal si hacemos algo más genérico que nos permita reemplazar cualquier palabra en cualquier texto.

```js
let reemplace = function(original, reemplazo) {
  return (texto) => texto.replace(original,reemplazo);
};

const reemplacePorPython = reemplace(/javascript/ig, ‘python’);
const reemplacePorGo = reemplace(/javascript/ig, ‘GO’);

console.log(reemplacePorPython(“JavaScript es un buen lenguaje”));
console.log(reemplacePorGo(“JavaScript es un buen lenguaje”));
```

La función *reemplace*, recibe un texto original y el texto que lo va a reemplazar, retorna una función que recibe un texto y reemplaza estos valores.

Luego creamos dos funciones, utilizando como template nuestra función *reemplace*. ¡Genial!

Esto nos permite hacer nuestro código más versátil y extensible.

Claro para entender cómo funciona esto debemos conocer algunos otros conceptos, pero en general ya con esto se pueden hacer muchas cosas, las cuales espero me permitan ver.

Seguiremos hablando de esto en los siguientes post.

[Aqui](https://jsbin.com/nuqatu/12/edit?js,console) el codigo del ejemplo
