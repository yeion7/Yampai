#Entendiendo la asignación por destructuring en JavaScript

*Destructuring* es una de las más poderosas características añadidas al lenguaje en ES2015, una característica que nos facilita las cosas y hace nuestro código más legible.

![](https://medium2.global.ssl.fastly.net/max/2048/1*A0A1oe9YdL4DppOfMZ0Iug.png)

*Destructuring* nos da una manera de extraer datos de objetos o arreglos y asignarlos a variables.

###Arrays

Imaginemos que asignamos un array con tres elementos

```js
const array = [‘pato’, ‘ganzo’, ‘pollo’];
```

Si en ES5 quisiéramos asignar los valores a variables deberíamos hacerlo de la manera

```js
var primer = array[0];

var segundo = array[1];

var tercero = array[2];
```

Pero con la función de *destructuring* en ES2015 lo haríamos de la manera:

```js
const [a,b,c] = array;
// a = 'pato'
// b = 'ganzo'
// c = 'pollo
```

Genial! Bastante más simple y legible, pero que tal si quisiéramos ignorar un elemento, podríamos realizar la asignación de la siguiente forma:

```js
const [a,,c] = array;

// a = 'pato'
// c = 'pollo'
```

Existe un caso de uso bastante útil, imagina que tienes dos variables y deseas intercambiar su valor, en ES5 tendríamos que crear una variable temporal para esto, pero con *destructuring* bastaría con hacer:

```js
let x = 2;
let y = 5;

[x,y] = [y,x];

// x = 5
// y = 2
```
Bastante más útil y legible, ¿cierto?

¿Crees que podría funcionar en arrays que son retornados por una función? que tal si lo pruebas y me cuentas.

###Objetos

Así como con los arrays, con objetos también podemos utilizar las características de *destructuring*, imaginemos un objeto de la forma

```js
const objeto = {
  a: ‘casa’,
  b: ‘apartamento’
};
```

Como asignariamos las propiedades de* objeto* a variables en ES5

```js
var a = objeto.a;
var b = objeto.b;
```

Con *destructuring* en ES2015, lo hariamos asi

```js
const {a,b} = objeto;

//a = 'casa'
//b = 'apartamento'
```

Si quisiéramos asignar las propiedades del objeto, con nombres de variable diferentes, lo hacemos de la forma

```js
const {a:uno,b:dos} = objeto;

//uno = 'casa'
//dos = 'apartamento'
```
Sabiendo esto, hagamos algo útil.

###**Valores por defecto en funciones**

Si tenemos una función que recibe un objeto como parámetro y quisiéramos establecer valores por defecto en ES5 lo hariamos asi

```js
function hablar(datos){
  datos = datos === undefined ? {} : opciones;
  nombre = datos.nombre === undefined ? ‘Yeison’ : opciones.nombre;
  pais = datos.pais === undefined ? ‘colombia’ : opciones.pais;

  console.log(‘Hola soy ‘ + nombre + ‘ y vivo en ‘ + pais);
}

hablar();
```

No se ve del todo bien ¿cierto?, pero con *destructuring* podríamos hacer algo así:

```js
function hablar({nombre = ‘yeison’, pais =’colombia’} = {}){
  console.log(`Hola soy ${nombre} y vivo en ${pais}`);
}

//Hola soy yeison y vivo en colombia
```

Es bastante más legible, y si quisiéramos imprimir otros valores, simplemente pasamos como parámetro de la función un objeto con los valores de las propiedades que queremos

```js
hablar({
  nombre: ‘felipe’,
  pais: ‘argentina’
});

//Hola soy felipe y vivo en argentina
```
###Objetos

####Manejando objetos anidados

```js
const yeison = {
  id: 27,
  user: ‘yeion7’,
  datos: {
  nombre: ‘Yeison’,
  apellido: ‘Daza’,
  edad: ‘22’
 }
}

function decirNombre(
 {
   user: nickName,
   datos:{ nombre: primerNombre }
 }) {

   console.log(`El usuario ${nickName} se llama ${primerNombre}`);
}

decirNombre(yeison);
```
