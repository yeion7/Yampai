
#var, let y const en JavaScript

##En JavaScript tenemos varias maneras de poder declarar nuestras variables, pero, ¿cuál deberías usar?

##var, let y const en JavaScript

En JavaScript tenemos varias maneras de poder declarar nuestras variables, pero, ¿cuál deberías usar?

![](https://medium2.global.ssl.fastly.net/max/2048/1*_iEpUDh2frt7Z3femLEeow.png)**

Como sabemos dependiendo de la manera en que declaremos nuestras variables, van a tener diferente scope.
> Si las declaramos con **var**, tienen un scope local.
> Si las declaramos con **let** o **const**, tienen un scope de bloque.
> [Entendiendo el scope de variables en JavaScript](https://medium.com/@yeion7/entendiendo-scopes-de-variables-en-javascript-661ea382c8bc)

Pero veamos otras consideraciones para saber como declarar nuestras variables

###Funcionamiento

* con ***var*** definimos una variable con local scope, también nos permite utilizar un comportamiento llamado [hoisting](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting), sin generar ningún error.

* con ***let*** definimos variable con block scope, las variables declaradas de esta manera nos genera un error de referencia cuando intentamos utilizar hoisting.

* con ***const*** definimos variables de sólo lectura (no confundir con inmutables), esto quiere decir que, cuando asignamos una variable, el nombre de esta va estar asignada a un puntero en memoria, el cual no puede ser sobreescrito o reasignado.

    const variable = 'esto';

    variable = 'eso'; // TypeError: Assignment to constant variable

Pero, si creamos un objeto con ***const*** y intentamos cambiar una de sus propiedades

    const variable = { cosa: ‘esto’};

    variable.cosa = ‘eso’;

    console.log(variable.cosa); //eso

Debido a esto existe confusión sobre el comportamiento de las variables declaradas con ***const***.

Como dije antes es una variable de sólo lectura, que no puede reasignarse el puntero en memoria, pero las cosas dentro de los valores por referencia si pueden ser modificadas.

Con valores primitivos como string o números, no podrán ser modificados.

###Legibilidad

Un aspecto fundamental de nuestro código es la legibilidad y lo entendible que sea a la hora de leerse por otros desarrolladores o nosotros mismos en el futuro, por eso considero que ***let*** y ***const*** es un paso adelante en este sentido.
> #Una variable debería ser usada para representar solo una cosa

Por eso, estoy a favor de ***const*** sobre ***let*** y ***var***, ya que este nos permite declarar una sola cosa por variable, dándonos a entender que durante la ejecución de nuestro código no será reasignado.

Así, ***let*** debería ser utilizado para variables dentro de loops o implementaciones de algoritmos como [swap](https://en.wikipedia.org/wiki/Swap_(computer_science)), donde se requiere intercambiar el valor de dos variables.

Una herramienta poderosa que puedes utilizar para mejorar tu código en este y otros aspectos es un Linter, en especial recomiendo [ESLint](http://eslint.org/) junto con las [guías de estilo para escribir código del equipo de airbnb](https://www.npmjs.com/package/eslint-config-airbnb).

¿Quieres saber más de este u otros temas sobre JavaScript?, sigue nuestros encuentros quincenales en [HangoutJS](https://twitter.com/HangoutJs) donde hablamos en comunidad y aprendemos compartiendo conocimiento.

[Aquí nuestros anteriores encuentros.](https://www.youtube.com/playlist?list=PLH3EFUtS4FBzUYU6BSouy0kiX3cnzyTKc)
