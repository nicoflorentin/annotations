---
tags: [Coderhouse, JavaScript]
title: '[JavaScript Clase 6] Arrays'
created: '2021-07-02T21:09:48.327Z'
modified: '2021-08-05T14:35:26.786Z'
---

# [JavaScript Clase 6] Arrays

## Array

**Un Array es una objeto que almacena una lista de elementos**. Puede ser un conjunto de números, strings, booleanos, objetos o hasta una lista de listas. 
Los valores del array pueden ser distintos y **es posible agregar o quitar elemento** en todo momento.
Los elementos del array tienen un íncice, de 0 (el primer elemento del array) hasta  el último elemento.

### Declaración de array

Para declarar un variable y asignar un array empleamos los corchetes **([ ])** y dentro definimos todos los valores **separados por coma**.
Los arrays en Javascript empiezan siempre en la posición 0, así que un array que tenga por ejemplo 10 elementos, tendrá posiciones de 0 a  9.

```javascript
// Declaraciòn de array vacío
const arrayA = [];
// Declaracion de array con nùmeros
const arrayB = [1,2];
// Declaracion de array con strings
const arrayC = ["C1","C2","C3"];
// Declaracion de array con booleanos
const arrayD = [true,false,true,false];
// Declaracion de array mixto
const arrayE = [1,false,"C4"];
```

### Acceso al array

Podemos acceder a los elementos empleando Array indicando su posición.
**A los números de las posiciones que usamos para acceder a los elementos del array se los puede llamar índices**. 

```javascript
const  numeros = [1,2,3,4,5];
let resultado1  = numeros[0] + numeros[2]; // 1 + 3 = 4; 
let resultado2  = numeros[1] + numeros[4]; // 2 + 5 = 7;
let resultado3  = numeros[1] + numeros[1]; // 2 + 2 = 4;
```

### Recorrido del array

Decimos que estamos recorriendo un Array **cuando empleamos un bucle para acceder a cada elemento**.
Los Array en JavaScript son objetos **iterables**, lo que permite usar distintas estructuras para iterar sobre ellos.

```javascript
const numeros = [1, 2, 3, 4, 5];
for (let index = 0; index < 5; index++) {
    alert(numeros[index]);
}
```

### Métodos comunes de los arrays

#### Metodos y propiedades mas comunes de los arrays

- Conocer el largo de un array: length
- Pasar a String: toString()
- Agregar elementos: push()
- Juntar los elementos separándolos por un caracter: join()
- Combinar dos Arrays en uno: concat()
- Generar un nuevo Array a partir de un rango de posiciones:  slice()

#### length

Al igual que en un String, la propiedad length nos sirve **para obtener el largo de un Array**, es decir, cuántos elementos tiene.

```javascript
const miArray = ["marca", 3 ,"palabra"];
console.log( miArray.length ); //imprime 3
```

#### toString

El método toString **convierte un Array a un String**, compuesto por cada uno de los elementos del Array separados por comas.

```javascript
const miArray = ["marca", 3 ,"palabra"];
console.log( miArray.toString() ); //imprime "marca,3,palabra"
```

#### push

**Para sumar un elemento a un Array ya existente**, se utiliza el método push, pasando como parámetro el valor (o variable) a agregar.

```javascript
const miArray = ["marca", 3, "palabra"];
miArray.push('otro elemento');
console.log(miArray.length); //El array ahora tiene 4 posiciones
```

#### join

Mediante el método join podemos **juntar todos los elementos de un Array en una cadena String**, indicando como parámetro el separador para esos elementos:

```javascript
const otroArray = ["hola", 22, "mundo"];
console.log(otroArray.join("*")); //Imprime "hola*22*mundo"
```

#### concat

Mediante el método concat podemos **combinar dos Arrays en un único Array** resultante:

```javascript
const miArray    = ["ford", 45];
const otroArray  = ["hola", 22, "mundo"];
const nuevoArray = miArray.concat(otroArray);
// nuevoArray ahora es igual a[ford,45,hola,22,mundo]
```

#### slice

**Devuelve una copia de una parte del Array dentro de un nuevo Array**, empezando por inicio hasta fin (fin no incluído). El Array original no se modificará.

```javascript
const nombres    = ['Rita', 'Pedro', 'Miguel', 'Ana', 'Vanesa'];
const masculinos = nombres.slice(1, 3); // Nuevo array desde la posición 1 a 3.
// masculinos contiene ['Pedro','Miguel']
```

### Ejemplo aplicado

```javascript
//Declaraciòn de array vacío y variable para determinar cantidad
const listaNombres = [];
let   cantidad     = 5;
//Empleo de do...while para cargar nombres en el array por prompt()
do{
   let entrada = prompt("Ingresar nombre");
   listaNombres.push(entrada.toUpperCase());
   console.log(listaNombres.length);
}while(listaNombres.length != cantidad)
//Concatenamos un nuevo array de dos elementos
const nuevaLista = listaNombres.concat(["ANA","EMA"]);
//Salida con salto de línea usando join
alert(nuevaLista.join("\n"));
```

## Arrays de objetos

Los array pueden usarse para almacenar objetos personalizados. **Podemos asignar objetos literales o previamente instanciados** en la declaración del array **o agregar nuevos objetos usando el método push** y el constructor

```javascript
const objeto1 = { id: 1, producto: "Arroz" };
const array   = [objeto1, { id: 2, producto: "Fideo" }];
array.push({ id: 3, producto: "Pan" });
```

#### for of

La sentencia sentencia for...of permite recorrer un objeto iterable (array) **ejecutando un bloque de código por cada elemento del objeto**.

```javascript
const productos = [{ id: 1, producto: "Arroz" },
                  { id: 2,  producto: "Fideo" },
                  { id: 3,  producto: "Pan" }];

for (const producto of productos) {
    console.log(producto.id);
    console.log(producto.producto);
}
```

#### type of

El operador typeof **devuelve una cadena que indica el tipo de dato del parámetro**. El parámetro puede ser una cadena, número, variable, u objeto. Sirve para detectar qué tipo de dato es el parámetro. Por ejemplo, chequear antes de quitar espacios, que efectivamente sea un string.

```javascript
let miFuncion = (a,b) => a + b;
let forma = " redonda ";
let tamano = 1;
console.log ( typeof miFuncion ); //imprime function
console.log ( typeof forma ); //imprime string 
console.log ( typeof tamano ); //imprime number

if (typeof forma == 'string')
    forma = forma.trim();
```

### Ejemplo aplicado con objetos, producto y array

```javascript
  class Producto {
    constructor(nombre, precio) {
        this.nombre  = nombre.toUpperCase();
        this.precio  = parseFloat(precio);
        this.vendido = false;
    }
    sumaIva() {
        this.precio = this.precio * 1.21;
    }
}
//Declaramos un array de productos para almacenar objetos
const productos = [];
productos.push(new Producto("arroz", "125"));
productos.push(new Producto("fideo", "70"));
productos.push(new Producto("pan", "50"));
//Iteramos el array con for...of para modificarlos a todos
for (const producto of productos)
    producto.sumaIva();
```

## Métodos de búsqueda y transformación

#### find

El método find()** devuelve el valor del primer elemento del Array que satisface la función de comprobación** enviada por parámetro. Si ningún valor satisface la función de comprobación, se devuelve undefined.

```javascript
const numeros    = [1, 2, 3, 4, 5];
//La función parámetro generalmente es una función flecha sin cuerpo.
const encontrado = numeros.find(elemento => elemento > 3); //Encuentra 4

const nombres     = ["Ana", "Ema", "Juan"];
const encontrado2 = nombres.find(elemento => elemento === "Ema"); //Encuentra "Ema"
const encontrado3 = nombres.find(elemento => elemento === "Alan");//undefined
```

#### filter

El método filter() **crea un nuevo Array con todos los elementos que cumplan la función de comprobación** enviada por parámetro. Generalmente, se obtiene un Array con menos elementos que la lista a filtrar.

```javascript
const numeros = [1, 2, 3, 4, 5];
const filtro1 = numeros.filter(elemento => elemento > 3); //Encuentra [4,5]
const filtro2 = numeros.filter(elemento => elemento < 4); //Encuentra [1,2,3]

const nombres = ["Ana", "Ema", "Juan", "Elia"];
//Filtrar nombre que incluyen la letra "n" Encuentra ["Ana","Juan"]
const filtro3 = nombres.filter(elemento => elemento.includes("n"));
```
#### map

El método map() **se utiliza para crear un nuevo Array con todos los elementos del Array original transformados según las operaciones** de la función enviada por parámetro. El nuevo Array obtenido tiene la misma cantidad de elementos que el array original pero con los valores modificados.

```javascript
const numeros  = [1, 2, 3, 4, 5];
const porDos   = numeros.map(x => x * 2);   // porDos = [2, 4, 6, 8, 10]
const masCien  = porDos.map(x => x + 100); // masCien = [102, 104, 106, 108, 110]

const nombres = ["Ana", "Ema", "Juan", "Elia"];
const lengths = nombres.map(nombre => nombre.length);//lengths = [3, 3, 4, 4]
```

### Ejemplo aplicado: buscando y filtrando objetos

```javascript
const productos = [{ id: 1,  producto: "Arroz", precio: 125 },
                  {  id: 2,  producto: "Fideo", precio: 70 },
                  {  id: 3,  producto: "Pan"  , precio: 50},
                  {  id: 4,  producto: "Flan" , precio: 100}];

const buscarPan = productos.find(producto => producto.id === 3); 
console.log(buscarPan);//{id: 3, producto: "Pan", precio: 50}

const baratos = productos.filter(producto => producto.precio < 100); 
console.log(baratos);//
[{id: 2,producto:"Fideo",precio:70},{id:3,producto:"Pan",precio: 50}]

const aumentos = productos.map(producto => producto.precio += 30);
console.log(aumentos);
//[155, 100, 80, 130] y el valor de cada producto cambio.
```


