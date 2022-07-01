## Clase 3 - Mutable o Inmutable

En JS los datos asignados a una variable pueden ser de dos tipos:

Primitive type (undefined, null, boolean, number, string, symbol), Reference type (objects, arrays , functions).

Una de las diferencia entre estas dos, est� en la forma como se almacenan estos datos en memoria, para ser m�s claro un ejemplo.

```
let name = 'Javier';
let name2 = name;
let person = {name: 'javier'};
let person2 = person;
```

Cuando creamos name js crea un espacio en memoria y guarda su valor, ahora cuando creamos name2 js contin�a crea un nuevo espacio en memoria y asigna el mismo valor de la varible name de esta forma el valor de la variable name2 es totalmente independiente a name.

Ahora si creamos la variable person como un objeto que contiene un name, y si luego creamos otra variable person2 y le asignamos el mismo objeto person, aqu� es donde la cosa cambia con respectos a los datos primitivos, en este caso js guardara el objeto person2 como una referencia o apuntador al objeto person, es decir que ambas variables apuntan al mismo objeto en memoria.

Ahora si entendamos Mutable o Inmutable.

Mutable: es algo que se puede cambiar o agregar.

Inmutable: es algo que no puede cambiar ni agregar.

Los valores primitivos en js son algo agregado donde solo se pueden reasignar y por lo tanto, todos estos valores son inmutables. Entendamos con un ejemplo.

```
console.log(name); //javier
console.log(name2); //javier

name2 = 'platzi';

console.log(name); //javier
console.log(name2); //platzi''
```

Si imprimimos name y name2, ambas nos dan javier, pero si reasignamos un valor de name2 y volvemos a imprimir ocurre que solo cambia el valor de name2, lo que demuestra que js guardas est�s variables de forma separada, aun cuando el valor de name2 se copio de name. Por eso los valores primitivos son inmutables.

ahora hagamos lo mismo con los objetos.

```

console.log(person); //{name: 'javier'}
console.log(person2); //{name: 'javier'}

person2.name = 'platzi';

console.log(person); //{name: 'platzi'}
console.log(person2); //{name: 'platzi'}
```

Al inicio obtenemos las mismas propiedades, ahora cambiemos una de las valores de las propiedades y veremos que js cambio el valor tanto de person y peron2, esto debido a que person2 se creo haciendo referencia al objeto person, con reference type js crea una referencia al mismo objeto y el objeto permanece mutable.

ya que el mismo objeto es mutable se puede cambiar o se pueden agregar nuevas propiedades al mismo objeto.

En es6 se creo un operador de propagaci�n que permirte copias un objeto de forma segura sin hacer referencia al mismo objeto y ser�a as�.

```
let person2 = {...person}
```

Ahora vuelve a ver la clase y veras como todo es m�s claro y entendible.

## clase 4 - Map

Lo más sencillo:

¿Qué hace el .map()? TRANSFORMAR.

.map() es INMUTABLE por lo tanto no modifica el array original, sino que crea uno nuevo con la “transformación” aplicada.
.
Además, mantienes el mismo length que el array original, te devuelve en el nuevo array la misma cantidad que el array que le aplicaste el método.
.
Código de la clase:

```

const products = [
            { title: 'Burger', price: 121 },
            { title: 'Pizza', price: 202 },
        ];
        const app = document.getElementById('app');
        const list = products.map(product => {
            return `<li>${product.title} - ${product.price}</li>`;
        })

        app.innerHTML = list.join('');
```

El método join() une todos los elementos de una matriz (o un objeto similar a una matriz) en una cadena y devuelve esta cadena.

```

const elements = ['Fire', 'Air', 'Water'];

console.log(elements.join());
// expected "Fire,Air,Water"

console.log(elements.join(''));
// expected  "FireAirWater"

console.log(elements.join('-'));
// expected "Fire-Air-Water"

```

Diferencia práctica entre .forEach()y .map()
Por si llegan a preguntárselo, si, éstos métodos son muy parecidos, ya que ejecutan una función sobre cada elemento de un array, pero hay una diferencia fundamental: .forEach() no crea o devuelve, por defecto, un nuevo array con los elementos modificados, en cambio .map() si.

## Clase 6 - map reloaded

Usos comunes o cl�sicos de map() sobre los arrays:

Limpiar datos, seleccionar datos dentro de un array y devolverlos para su utilizaci�n en futuras acciones.
A�adir un nuevo elemento, modificar agregando un nuevo dato al objeto pero sin modificar el array original.

Tener en cuenta que cuando trabajamos con objetos y map() y retornamos el mismo objeto estamos copiando la referencia en memoria que tiene el objeto original que le aplicamos el map() (esto lo vimos en la clase de mutable vs inmutable, te dejo una lectura: https://platzi.com/tutoriales/1642-javascript-profesional/4559-estructuras-de-datos-inmutables/). Esto provoca que como estamos modificando la referencia en memoria, el array original tambi�n sea modificado. Entonces en conclusi�n, por m�s que map() sea inmutable en este punto estamos copiando la referencia en memoria y por eso hace el cambio en el original.

```
// Estamos retornando el objeto
// por ende se copia la refencia en memoria
const rta = orders.map(item => {
    item.tax = .19
    return item;
})
```

Para evitarlo, y poder realizar una copia y evitar la referencia en memoria, utilizamos el spread operator de ES6 (https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Operators/Spread_syntax), donde generamos un nuevo objeto con los valores del objeto original y luego agregamos el nuevo valor que nos interesa.

```
const rta = orders.map(item => {
    // retornamos un nuevo objeto
    //pero evitamos hacer ref. en memoria
    return {
        ...item,
        tax: .19,
    }
})
```

## Clase 8 - filter

filter() lo que hace es filtrar el array original en base a una condici�n, los que la cumplan estaran en el nuevo array creado.
.
Por lo tanto filter() es inmutable y el nuevo array creado solamente puede contener:

cero coincidencias
todas coincidencias
algunas coincidencias
Pero nunca m�s coincidencias que el tama�o del array original.

```
const words = ["spray", "limit", "elite", "exuberant"];

// con for
const newArray = [];
for (let index = 0; index < words.length; index++) {
  const element = words[index];
  if (element.length >= 6) {
    newArray.push(element);
  }
}

// VS

// con filter
const rta = words.filter((element) => element.length >= 6);

// en ambos casos, el resultado:
> [ 'exuberant' ]
```

offtopic: el m�todo includes() determina si una matriz incluye un determinado elemento, devuelve true o false seg�n corresponda.

```

const array1 = [1, 2, 3];

console.log(array1.includes(2)); // expected truee

const pets = ['cat', 'dog', 'bat'];

console.log(pets.includes('cat')); // expected true

console.log(pets.includes('at')); // expected false

```

## Clase 10 - Reduce

Este m�todo REDUCE, efectivamente hace eso. Solo reduce a un solo valor y no devuelve otro array, simplemente un valor.

Se utiliza much�simo para hacer c�lculos a partir de la informaci�n de un array.

En su composici�n, a primeras, tiene como argumentos de la funci�n del primer par�metro, al acumulador y como segundo par�metro al elemento por el que va iterando el loop. Y como segundo argumento del reduce(), se pasa el valor inicial del acumulador.

```

const totals = [1,2,3,4];
// primer argumento de la f() es el acumulador
// segundo argumento de la f() es el elemento
// segundo par�metro de la f() es el estado inicial del acumulador
const rta = totals.reduce((sum, element) => sum + element, 0);
console.log(rta)
```
