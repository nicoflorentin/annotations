---
tags: [JavaScript]
title: '[JavaScript] Map, Filter y Reduce'
created: '2022-09-09T16:29:22.664Z'
modified: '2022-09-13T03:23:33.556Z'
---

# [JavaScript] Map, Filter y Reduce

Nuestros programas comienzan con valores iniciales y los vamos modificando sin cambiar los valores iniciales, si no que creando nuevas variables, mutaciones de la variable inicial.

- Funciones de orden superior : Funciones **reciben por parámetros otras funciones** o funciones que como resultado de su ejecucion **retornan otra funcion**

## MAP

Tenemos un array y queremos obtener un nuevo array de otra cosa
```js
const numeros = [1,2,3,4,5]
const dobles = numeros.map( (num)  => { return num*2 } )
```
Otra manera : 
```js
const numeros = [1,2,3,4,5]
const dobles = numeros.map( num  => num*2 )
```
 
## FILTER

El método filter() crea un nuevo array con todos los elementos que cumplan la condición implementada por la función dada.

```js
const words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];
const result = words.filter( word => word.length > 6);
console.log(result);
// expected output: Array ["exuberant", "destruction", "present"]
```

```js
function esSuficientementeGrande(elemento) {
  return elemento >= 10;
}
var filtrados = [12, 5, 8, 130, 44].filter(esSuficientementeGrande);
// filtrados es [12, 130, 44]
```

## REDUCE

**Reduce el array original a un único valor.** Recibe dos parámetros, función acumuladora y valor inicial del acumulador.

```js
const numeros = [3,10,20,50]
let total = numeros.reduce( (acumulador , numero)=>{ 
  return acumulador + numero
}, 0)
```

**Lo que retorna la funcion acumuladora va a ser el acumulador en la siguiente iteración.**

Tambien puede recibir dos parámetros mas:

```js
let newArray = numeros.reduce( acc, num, index, array ) {
  //code
}
```

Donde "acc" es el acumulador, "num" es el elemento iterado, "index" es el índice del elemento iterado, y "array" es el array completo con todos sus elementos.

