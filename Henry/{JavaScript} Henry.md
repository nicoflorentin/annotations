Resolver booleano de un dato : 

```js
!!'cadena' ; // true
!! '' // false
!! 150 // true
!! 0 //false
```

### Scope

**Cada contexto maneja sus propias variables**, y son independientes de los demás. Justamente por eso, podemos usar los mismos nombres de variables dentro de funciones que creamos sin que _pisen_ las demás. También sabemos que podemos acceder a una variable declarada en el contexto global dentro de una función. **Esto se debe a que JavaScript primero busca una variable dentro del contexto que se está ejecutando, si no la encuentra ahí, usa la referencia al `outer context` para buscarla dentro de ese contexto**. Gracias a esto vamos a poder acceder a variables que estén afuera de nuestro contexto (siempre y cuando no hayamos declarado una nueva con el mismo nombre!!).

Veamos en el código siguiente el comportamiento de las variables:
```js
var global = 'Hola!';

function a() {
  // como no hay una variable llamada global en este contexto,
  // busca en el outer que es el global
  console.log(global); 
  global = 'Hello!'; // cambia la variable del contexto global
}

function b(){
  // declaramos una variable global en nuestro contexto
  // esta es independiente 
  var global = 'Chao'; 
  console.log(global);
}

a(); // 'Hola!'
b(); // 'Chao'
console.log(global); // 'Hello'
```
### Precedencia de Operadores y Asociatividad

Ahora si tuvieramos la misma precedencia entraría en juego la asociatividad, veamos un ejemplo:

```js
var a = 1, b = 2, c = 3;

a = b = c;

console.log(a, b, c);
```

Para eso tenemos que revisar la tabla por la asociatividad del ***operador de asignación `=`. Este tiene una precedencia de 3 y una asociatividad de `right-to-left`***, es decir que las operaciones se realizan primero de derecha a izquierda. En este caso, primero se realiza `b = c` y luego `a = b` (en realidad al resultado de `b = c`, que retorna el valor que se está asignando). Por lo tanto al final de todo, todas las variable van a tener el valor `3`. Si la asociatividad hubiese al revés, todos las variables tendrían el valor `1`.

### Closures

Los closures son funciones que retornan otra función y utilizan variables "encerradas" que solo pueden ser modificadas por la funcion que se retorna.

```js
function hacerSaludo( lenguaje ){
  return function(){
    if ( lenguaje === 'en'){
      console.log('Hi!');
    }

    if ( lenguaje === 'es'){
      console.log('Hola!');
    }
  }
}

var saludoIngles = hacerSaludo('en');
var saludoEspaniol = hacerSaludo('es');
```

## Call, Apply and Bind

Todas las funciones tienen acceso a los métodos:

-   call() = Copia de la funcion y la ejecuta al instante
-   bind() = Copia de la funcion pero no la ejecuta
-   apply() = Copia de la funcion , la ejecuta al instante y recibe un array como argumento

Justamente invocando estos métodos vamos a poder tener control sobre el keyword `this`. Veamos algunos ejemplos:
```js
var persona = {
  nombre: 'Franco',
  apellido: 'Chequer',

  getNombre: function(){
    var nombreCompleto = this.nombre + ' ' + this.apellido;
    return nombreCompleto;
  }
}

var logNombre = function(){
  console.log(this.getNombre());
}
```
**La función `bind()` devuelve una copia de la función, la cúal tiene internamente asociado el keyword `this` al objeto que le pasemos por parámetro.** 
```js
var logNombrePersona = logNombre.bind(persona);
logNombrePersona();
```
Se puede usar para copiar la funcion pero con argumentos dinámicos, y luego cuando se llama a la copia le pasamos el resto de los argumentos.

## Recursividad



### Números Naturales (N)

¿Como podríamos armar una función recursiva con estas propiedades?
```js
function esNatural(num) {
    // planteo el caso base en el que llegamos a 0
    if(num === 0) return true
    // si no le pregunto si `num-1` es natural
    // lógicamente este ciclo se repetirá hasta llegar a 0
    return esNatural(num-1)
}
```
¿Qué paso? `Maximum call stack size exceeded` parece que **superamos la cantidad de scopes posibles** que podíamos generar al stack del `Event Loop`, esto se llama un _**stack overflow**_. Eso significa o que pedimos un número muy grande que no llego a terminar de resolverlo, o que se nos escapo un caso en el que debería cortar la recursion.

Solución : 
```js
function esNatural(num) {
    if(num === 0) return true;
    // agrego una nueva condición para que no se pase de 0
    if(num < 0) return false;
    return esNatural(num-1);
  }

// esNatural(5) true
// esNatural(-2) false
// esNatural(1.5) false
```
**Una de las contras que tiene este método es lo grave que son las fallas**, como vieron, por olvidarnos un caso puede que creamos que el programa funciona correctamente y cuando no encontremos con situaciones no contempladas podemos colgar todo el programa sin poder detectar el error y trabajarlo.

## Estructuras de Datos

Cuando hablamos a estructura de Datos nos referimos a cómo organizamos los datos cuando programamos. Básicamente, este tema trata de encontrar formas particulares de organizar datos de tal manera que puedan ser utilizados de manera eficiente.

Imaginen que los datos que tenemos que manejar son libros!, y en un principio tenemos muchísimos libros desordenados por casa. Cada vez que queremos leer un libro, tardamos dos horas buscando uno por uno hasta dar con el libro. Eso no es eficiente. Entonces, ¿qué hacemos? Bueno, podemos armar una biblioteca, por ejemplo, y acomodamos los libros en orden alfabético, esto nos ahorra tiempo en buscarlos. Y, ¿qué pasa si tenemos demasiados libros y no entran en una biblioteca? Podemos tener un lugar donde depositamos los libros que menos usamos, y mantenemos una libretita donde especificamos qué libros dejamos ahí y en que depósito están. En fin, podemos organizarlos de mil maneras, pero se entiende la idea que organizando los datos vamos a ser más eficientes, no?

## Arreglos

El arreglo es una colección finita de elementos que ocupan espacios contiguos de memoria, y se pueden acceder a cada uno de ellos a través de un índice.

**Pero no es tan bueno cuando tenemos que buscar un objeto en él, ya que tenemos que recorrerlo entero para encontrarlo. Borrar un elemento también es medio costoso.**

## Sets

Un Set es una colección de elementos sin un orden en particular en donde _cada elemento puede aparecer una sola vez_. 
```js
var arreglo = [1,2,3,4,4,5,5,1,2]
var set1    = new Set(arreglo)
console.log(arreglo)   // [ 1, 2, 3, 4, 4, 5, 5, 1, 2 ]
console.log(set1)      // Set { 1, 2, 3, 4, 5 }
```
## Pilas (Stack)

**El último que entra es el primero que va a salir**. Esto se conoce como una estructura tipo **LIFO**: _Last in, first out_.

Básicamente un stack tiene dos operaciones: `push()` y `pop()`, ya que sólo podés poner y sacar elementos en un orden definido, hace que no necesitemos más operaciones. Podemos usar múltiples formas de implementar una Pila en javascript. Lo podemos hacer usando arreglos, una lista enlazada, o bien crear nuestra propia clase Pila. Veamos como hacerlo usando arreglos:

```js
function Stack() {
  this.arr = [];
}

Stack.prototype.push = function (value) {
  this.arr.push(value);
};

​var miStack1 = new Stack();
miStack1.push(5);

var miStack2 = new Stack();
miStack2.push(10);

console.log(miStack1);
console.log(miStack2);
```


## Cola (Queue)

Una cola, es una estructura en la cual el **primer elemento que entra es el primer elemento que sale,** y se conoce como estructura tipo **FIFO**: _First in, First out_. La cola tiene dos métodos tambien: `enqueue()` y `dequeue()`, que sirven para encolar y 'desencolar' elementos.
Se puede hacer de muchas maneras. Vamos a mostrar la más simple, con arreglos:
```js
var queue = [];
queue.push(1);         // la cola es [1]
queue.push(2);         // la cola es [1, 2]
var i = queue.shift(); // la cola es [2]
console.log(i);        // muestra 1
```
