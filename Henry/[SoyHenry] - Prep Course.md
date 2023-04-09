---
title: '[SoyHenry] - Prep Course'
created: '2023-01-10T17:23:35.044Z'
modified: '2023-01-11T17:13:34.516Z'
---
# Prep Course

Code review
Break 15'
Lecture
Break 1hr
Practice
Pair Programming
Stand Up

Los comandos de la terminal utilizan opciones con un guion y argumentos escritos sin simbolos.

comandos de linux
pwd indica carpeta actual
ls directorios
cd cambiar directorio
cd .. atras
clear borra consola
mkdir crear carpeta
touch crea archivo vacio
rm elimina archivo indicado
rm -r elimina carpeta o directoio indicado
help larga lista de comandos basicos
ls -- help ayuda sobre el comando ls

los archivos staged de git se guardan en la memoria ram

git restore 'archivo 1.txt' para borrar las modificaciones a un archivo




Tipos de datos de Javascript

String
Number
Boolean
Undefined (variable declarada pero no inicializada)
Null (variable declarada que tiene asignado el valor null)

Operadores principales y su precedencia
+ suma
- rest
* multuiplicacion
/ division
% resto



Operadores de comparacion
 
> mayor
< menor
>= mayor igual
<= menor igual
== igual
!= distinto

= operador de asignacion
== igual valor [abstract equality comparision]
=== [igualdad estricta] igual valor y tipo (se puede comparar un numero 3 con una cadena '3')

c = a = b (primero a = b y luego c = a) se mira desde la derecha
16 / 2 / 4 (primero 16/2 luego 8/4) se mira desde la izquierda


Funciones

```js
function sumaTres(x) {
  return(x + 3)
}
```
todo lo que esta debajo del return no se ejecura jamás
si la funcion no tiene retorno, esta retorna undefined
en ningun programa real debe haber un console.log()




Nomenclaturas

camelCase
PascalCase
snake_case




Operadores logicos

&& and
|| or
! not





Veracidad

1           // true
0           // false
-1          // true
true        // true
false       // false
'string'    // true
null        // false
undefined   // false
[ ]          // true





Bucles for y while

for recibe : 
variable
condicion
accion

```js
suma = 0 ;
for (var i=0 ; i < 10 ; i++) {
  suma = suma + 1 ;
  console.log(suma)
}
```

while recibe : 
condicion
```js
while (i < 2) {
  console.log(i)
}
```

mas...

switch
do-while
declaracion continue
break





Array o Matriz

array de elementos
indice arranca de 0, posicion del dato
si creo un elemento en array[3], entonces el indice 0, 1, 2 quedan vacíos
array.length retorna el number de cuantos elementos tiene el array




Metodos de array

array.split('') para separar la palabra en un nuevo array con el separador '' .
array.pop()
array.push('y')
array.join('') junta la palabra de nuevo en una cadena

array.forEach((num) => console.log(num)) ejecuta una linea de codigo por cada elemento del array

array.map() 

Metodos de insercion
push()
pop()
unshift()
shift()

includes()
every()
split()
join()

Metodos de recorrido
forEach()
map()





Bucles o ciclos en arrays

for(var i = 0; i < array.length; i++) {
  console.log(array[i])
}




Introduccion a objetos

```js
var objeto = {
  clave1: 'valor1',
  clave2: 'valor2'
}

//asignar valor
objeto.clave1 = 'valor3'

// borrar la clave1
delete objeto.clave1

// funciones dentro d eobjetos
var misFunciones = {
  saludar: function () {
    console.log('hola')
  }
} 
```



Dot notation y bracket notation

accedes a propiedades con un punto o con corchetes

```js
var objeto = {
  propiedad: 'valor'
}

// acceder a la propiedad
objeto.propiedad // 'valor'
objeto['propiedad'] // 'valor'
```





Objetos avanzados

```js
var objeto = {
  propiedad: 'valor'
  funcion: function() {
    console.log(this.propiedad)
  }
}
objeto.hasOwnProperty('propiedad') //true

Object.keys(objeto) //['propiedad']

for(var prop in objeto) {
  console.log(prop) //'propiedad'
  console.log(objeto[prop]) //'valor'
}


```





Clases

Entidades
Las clases son plantillas o modelos de una entidad

Maneras de declarar las clases :
funcion constructora
expresion de clase

### FUNCIÓN CONSTRUCTORA
```js
function Auto(puertas, color, marca, año, ruedas) {
   this.puertas = puertas;
   this.color = color;
   this.marca = marca;
   this.año = año;
   this.ruedas = ruedas;
}
let miPrimerAuto = new Auto(2, 'Rojo', 'Ferrari', 2018, 4);
console.log(miPrimerAuto);
console.log(miPrimerAuto.marca);
```

### EXPRESIÓN DE CLASE

```js
class Auto {
   constructor(puertas, color, marca, año, ruedas) {
      this.puertas = puertas;
      this.color = color;
      this.marca = marca;
      this.año = año;
      this.ruedas = ruedas;
   }
}
let miSegundoAuto = new Auto(4, 'Blanco', 'Fiat', 2015, 4);
console.log(miSegundoAuto);
console.log(miSegundoAuto.marca);
```

## Prototipos

Mecanismo por el cual todos los objetos de Javascript pueden extender sus propiedades o metodos
El proceso en el que los objetos globales de JavaScript le extienden métodos y propiedades a cualquier tipo de dato se denomina herencia. 

```js
Array.prototype.mayorQueTres = function () {
   var arregloModificado = [];
   for (var i = 0; i < this.length; i++) {
      	if (this[ i ] > 3) {
         		arregloModificado.push(false);
     	 } else {
        		 arregloModificado.push(this[ i ]);
     	 }
   }
   return arregloModificado;
};
 
var arreglo = [1, 2, 3, 4, 5];
var nuevoArreglo = arreglo.mayorQueTres();
console.log(nuevoArreglo);
class LatinoAmerica {
	constructor() {
		this.paises = [ ];
	};
};
 
LatinoAmerica.prototype.agregarPais = function (pais) {
   	this.paises.push(pais);
};
let continente = new LatinoAmerica();
continente.agregarPais('México');
console.log(continente.paises);
```





## Extension de clase

```js
class Persona {
   constructor(nombre, edad) {
      this.nombre = nombre;
      this.edad = edad;
   }
   saludar() {
      console.log(
         'Hola, mi nombre es  ' + this.nombre + '. Tengo  ' + this.edad
      );
   }
}
let martin = new Persona('Martin', 26);
martin.saludar();
class Programador extends Persona {
   constructor(nombre, edad, añosDeExperiencia) {
      super(nombre, edad);
      this.añosDeExperiencia = añosDeExperiencia;
   }
   codear() {
      console.log(
         'Soy ' +
            this.nombre +
            ' . Codeo desde hace  ' +
            this.añosDeExperiencia +
            ' años'
      );
   }
}

let martin = new Persona('Martín', 26);
let programador = new Programador('María', 37, 4);
martin.saludar();
programador.codear();
```





## Callbacks

Son funciones que se pasan por parametro a otras funciones

```js
function devuelvoUsuario() {
   return 'CAMILO';
}
function devuelvoSaludo() {
   return 'Hola';
}
function saludar(cb1, cb2) {
   return cb1() + ' ' + cb2();
}
var resultado = saludar(devuelvoSaludo, devuelvoUsuario);
console.log(resultado);
```

