## Clase 3 - Mutable o Inmutable

En JS los datos asignados a una variable pueden ser de dos tipos:

Primitive type (undefined, null, boolean, number, string, symbol), Reference type (objects, arrays , functions).

Una de las diferencia entre estas dos, esta en la forma como se almacenan estos datos en memoria, para ser mas claro un ejemplo.

```
let name = 'Javier';
let name2 = name;
let person = {name: 'javier'};
let person2 = person;
```

Cuando creamos name js crea un espacio en memoria y guarda su valor, ahora cuando creamos name2 js continua crea un nuevo espacio en memoria y asigna el mismo valor de la varible name de esta forma el valor de la variable name2 es totalmente independiente a name.

Ahora si creamos la variable person como un objeto que contiene un name, y si luego creamos otra variable person2 y le asignamos el mismo objeto person, aqui es donde la cosa cambia con respectos a los datos primitivos, en este caso js guardara el objeto person2 como una referencia o apuntador al objeto person, es decir que ambas variables apuntan al mismo objeto en memoria.

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

Si imprimimos name y name2, ambas nos dan javier, pero si reasignamos un valor de name2 y volvemos a imprimir ocurre que solo cambia el valor de name2, lo que demuestra que js guardas estas variables de forma separada, aun cuando el valor de name2 se copio de name. Por eso los valores primitivos son inmutables.

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

En es6 se creo un operador de propagaci??????n que permirte copias un objeto de forma segura sin hacer referencia al mismo objeto y ser??????a as??????.

```
let person2 = {...person}
```

Ahora vuelve a ver la clase y veras como todo es m???s claro y entendible.

## clase 4 - Map

Lo m??s sencillo:

??Qu?? hace el .map()? TRANSFORMAR.

.map() es INMUTABLE por lo tanto no modifica el array original, sino que crea uno nuevo con la ???transformaci??n??? aplicada.
.
Adem??s, mantienes el mismo length que el array original, te devuelve en el nuevo array la misma cantidad que el array que le aplicaste el m??todo.
.
C??digo de la clase:

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

El metodo join() une todos los elementos de una matriz (o un objeto similar a una matriz) en una cadena y devuelve esta cadena.

```

const elements = ['Fire', 'Air', 'Water'];

console.log(elements.join());
// expected "Fire,Air,Water"

console.log(elements.join(''));
// expected  "FireAirWater"

console.log(elements.join('-'));
// expected "Fire-Air-Water"

```

Diferencia pr??ctica entre .forEach()y .map()
Por si llegan a pregunt??rselo, si, ??stos m??todos son muy parecidos, ya que ejecutan una funci??n sobre cada elemento de un array, pero hay una diferencia fundamental: .forEach() no crea o devuelve, por defecto, un nuevo array con los elementos modificados, en cambio .map() si.

## Clase 6 - map reloaded

Usos comunes o cl??sicos de map() sobre los arrays:

Limpiar datos, seleccionar datos dentro de un array y devolverlos para su utilizaci??n en futuras acciones.
A??adir un nuevo elemento, modificar agregando un nuevo dato al objeto pero sin modificar el array original.

Tener en cuenta que cuando trabajamos con objetos y map() y retornamos el mismo objeto estamos copiando la referencia en memoria que tiene el objeto original que le aplicamos el map() (esto lo vimos en la clase de mutable vs inmutable, te dejo una lectura: https://platzi.com/tutoriales/1642-javascript-profesional/4559-estructuras-de-datos-inmutables/). Esto provoca que como estamos modificando la referencia en memoria, el array original tambi??n sea modificado. Entonces en conclusi??n, por m??s que map() sea inmutable en este punto estamos copiando la referencia en memoria y por eso hace el cambio en el original.

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

filter() lo que hace es filtrar el array original en base a una condici??n, los que la cumplan estaran en el nuevo array creado.
.
Por lo tanto filter() es inmutable y el nuevo array creado solamente puede contener:

cero coincidencias
todas coincidencias
algunas coincidencias
Pero nunca m??s coincidencias que el tama??o del array original.

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

offtopic: el m??todo includes() determina si una matriz incluye un determinado elemento, devuelve true o false seg??n corresponda.

```

const array1 = [1, 2, 3];

console.log(array1.includes(2)); // expected truee

const pets = ['cat', 'dog', 'bat'];

console.log(pets.includes('cat')); // expected true

console.log(pets.includes('at')); // expected false

```

## Clase 10 - Reduce

Este m??todo REDUCE, efectivamente hace eso. Solo reduce a un solo valor y no devuelve otro array, simplemente un valor.

Se utiliza much??simo para hacer c??lculos a partir de la informaci??n de un array.

En su composici??n, a primeras, tiene como argumentos de la funci??n del primer par??metro, al acumulador y como segundo par??metro al elemento por el que va iterando el loop. Y como segundo argumento del reduce(), se pasa el valor inicial del acumulador.

```

const totals = [1,2,3,4];
// primer argumento de la f() es el acumulador
// segundo argumento de la f() es el elemento
// segundo par??metro de la f() es el estado inicial del acumulador
const rta = totals.reduce((sum, element) => sum + element, 0);
console.log(rta)
```

## Clase 13 - Some

Este m??todo nos devuelve true o false s?? al menos 1 elemento de nuestro array cumple con la condici??n.

```
const array = [1, 2, 3, 4, 5];

const even = (element) => element % 2 === 0;

console.log(array.some(even)); // resultado true
```

Al d??a de hoy (21/9/21), la librer??a de fechas date-fns esta en la versi??n 2.24.0 y funciona correctamente el ejercicio. S?? vienes del futuro, recuerda instalar la versi??n que usa el profe para evitar incompatibilidades si es que la sintaxis o algo de la misma librer??a ha sido modificada.

## Clase 15 - Every

Este m??todo es el contrario a some(), devuelve true o false s?? TODOS los elementos del array cumplen la condici??n.

```
const isBelowThreshold = (currentValue) => currentValue < 40;

const array1 = [1, 30, 39, 29, 10, 13];

console.log(array1.every(isBelowThreshold)); // expected output: true

```

## Clase 16 - Find

El m??todo find() devuelve el primer elemento del array que cumpla con la condici??n dada o no devuelve undefined si es que no encuentra ning??n elemento que cumpla los requisitos pedidos.

```
const array1 = [5, 12, 8, 130, 44];

const found = array1.find(element => element > 10);
console.log(found);
// expected output: 12
```

En cambio el m??todo findIndex() es una variante que te devuelve el index o posici??n donde esta ese primer elemento que encuentra con las caracter??sticas de la condici??n dada. De no encontrar ninguno devuelve -1 como respuesta del return del m??todo.

```
const array1 = [5, 12, 8, 130, 44];

const isLargeNumber = (element) => element > 13;
console.log(array1.findIndex(isLargeNumber));
// expected output: 3
```

## Clase 17 - Include

El m??todo includes() determina si una array incluye un determinado elemento, devuelve true o false seg??n corresponda.

```
const array1 = [1, 2, 3];

console.log(array1.includes(2));
// expected output: true

const pets = ['cat', 'dog', 'bat'];

console.log(pets.includes('cat'));
// expected output: true

console.log(pets.includes('at'));
// expected output: false
```

Tambi??n posee un segundo par??metro que es el fromIndex, que es la posici??n donde comenzar a buscar el valor en el array.

```
[1, 2, 3].includes(2);     // true
[1, 2, 3].includes(4);     // false
[1, 2, 3].includes(3, 3);  // false
[1, 2, 3].includes(3, -1); // true
[1, 2, NaN].includes(NaN); // true
```

## clase 20 - Join

Este fromIndex s?? es igual o mayor que el tama??o del array, devuelve false automaticamente sin buscar en el vector. S?? el fromIndex es negativo busca en todo el array. Y para los casos 0, -0, +0 lo toma como cero y tambi??n lee todo el array.

El m??todo join() une todos los elementos de un array en una cadena y devuelve esta cadena. Podemos pasarle cualquier elemento como separador que deseemos.

```

const elements = ['Fire', 'Air', 'Water'];

console.log( elements.join() );
// expected output "Fire,Air,Water"

console.log(elements.join(''));
// expected output "FireAirWater"

console.log(elements.join('-')); // expected output "Fire-Air-Water"
```

Y el m??todo split() divide un objeto de tipo String en un array de cadenas mediante la separaci??n de la cadena en sub-cadenas. Ac?? esta muy bien explicado y con muchos ejemplos: https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/String/split

El metodo .splice(), no solamente sirve para borrar en cierta forma un elemento sino tambi??n para agregarlos al index del array que tu quieres.Ej:

Tenemos el siguiente array:

```
const holaMundo = [??Maria??, ??Andres??, ??Cecilia??];
```

Y quiz??s lo que quieres es a??adir a ??Roberto?? despu??s de Andres y antes de cecilia.

Buscamos el index con el findIndex de cecilia tal como el profe nos ense??o.

```
holaMundo.splice(index, 0, ??Roberto??)
```

y listo, pones tu index de celcilia, no le ponemos un 1 porque no queremos eliminar ning??n elemento hacia la derecha sino un 0, pones la coma y pones el o los elementos que quieres agregar all??.

## clase 22 - Concat
El m??todo concat() se usa para unir dos o m??s arrays. Este m??todo no cambia los arrays existentes, sino que devuelve un nuevo array.

Recordar que al ser inmutable, los arrays (tanto el nuevo como el viejo) quedaran referenciados por memoria, por lo tanto s?? modificamos alguno de los dos, los cambios se ver??n reflejados en ambos.

```
const array1 = ['a', 'b', 'c'];
const array2 = ['d', 'e', 'f'];
const array3 = array1.concat(array2);

console.log(array3);
// expected output: Array ["a", "b", "c", "d", "e", "f"]
```

Si estas trabajando con un arrays de Objs igual una forma de copiar cada elemento sin la referencia podr??a ser:

```
const newArray = myArray.map(a => ({??a}));
```

## clase 24-Flat y FlatMap

flatMap() es un m??todo que primero mapea cada elemento, y despu??s aplana el resultado en un nuevo array.
Es id??ntico a hacer un map() seguido de un flat() de profundidad 1.
Si necesitas hacer un flat de mayor profundidad, es mejor usar los m??todos por separado, en lugar de usar flatMap().

Usando flatMap como filtro
Con flatMap puedes filtrar elementos, por ejemplo:

```
const numbers = [1, 2, 3, -4, -3, -7];
filterNumbers = numbers.flatMap(number => {
   return number < 0 ? [] : [number]
});
console.log('Filtered Number', filterNumbers); // Filterd Numbers: [1,2,3]

```

Pero, ??c??mo funciona?
Funciona gracias al array vac??o, ejemplo:

```
const arr = [[], 1];
flattenedArray = arr.flat();
console.log('FLattened Array', flattenedArray); // Flattened Array: [1]

```

Cuando quieres aplanar un elemento que es un array vac??o, flat() simplemente remueve el array, por lo tanto, podemos usar flatMap para que se comporte como una especie de filtro si es que lo necesitamos. ????

## Clase 27 - Sort

El m??todo sort() ordena los elementos de un arreglo (array) localmente y devuelve el arreglo ordenado. La ordenaci??n no es necesariamente estable. El modo de ordenaci??n por defecto responde a la posici??n del valor del string de acuerdo a su valor Unicode.

```
arr.sort([compareFunction])
let frutas = ['guindas', 'manzanas', 'bananas'];
frutas.sort(); // ['bananas', 'guindas', 'manzanas']

let puntos = [1, 10, 2, 21];
puntos.sort(); // [1, 10, 2, 21]
// Tenga en cuenta que 10 viene antes que 2
// porque '10' viene antes que '2' seg??n la posici??n del valor Unicode.

let cosas = ['word', 'Word', '1 Word', '2 Words'];
cosas.sort(); // ['1 Word', '2 Words', 'Word', 'word']
// En Unicode, los n??meros vienen antes que las letras may??sculas
// y estas vienen antes que las letras min??sculas.

let arr = ['80', '9', '700', 40, 1, 5, 200];
function comparar(a, b) {
  return a - b;
}
console.log('original:', arr.join());
console.log('ordenado sin funci??n:', arr.sort());
console.log('ordenado con funci??n:', arr.sort(comparar));
```

??Por qu?? a - b o b - a?
La funci??n que le enviamos a sort es la funci??n compareFn donde:

Si compareFn(a, b) devuelve un valor mayor que 0, ordena b antes a.
Si compareFn(a, b) devuelve un valor menor que 0, ordena a antes b.
Si compareFn(a, b) devuelve 0 a y b se consideran iguales.
