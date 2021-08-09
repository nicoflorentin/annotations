---
tags: [Coderhouse, JavaScript]
title: '[JavaScript Clase 5] Objetos'
created: '2021-06-24T21:28:10.227Z'
modified: '2021-08-05T14:35:28.333Z'
---

# [JavaScript Clase 5] Objetos

## Qué es un objeto?

En programación, y también en JS, **un objeto es una colección de datos relacionados con funcionalidad**, que generalmente consta de variables, denominadas propiedades, y funciones asociadas, llamadas métodos.
Por ejemplo: el objeto persona, tendría como una propiedad la altura, y como un método, hablar.

Cuando tengo que crear un elemento cuya información está compuesta por más de un valor y existen operaciones comunes (funciones) para todos los elementos de este tipo y sus propiedades, debe definirse como un objeto.

```javascript
let nombre = "Homero";
let edad   = 39;
let calle  = "Av. Siempreviva 742";
// Los variables anteriores entran relacionados entre sí, entonces mejor usamos un objeto literal
const persona1 = { nombre: "Homero", edad: 39, calle: "Av. Siempreviva 742" }
```

### Obteniendo valores de un objeto

**Para obtener el valor de una propiedad en un objeto utilizamos la notación punto (.)**: El nombre de la variable del objeto, seguido de punto y el nombre de la propiedad.

#### Objeto literal:

```javascript
const persona1 = { nombre: "Homero",
                   edad: 39,
                   calle: "Av. Siempreviva 742"};
                   
console.log(persona1.nombre);
console.log(persona1.edad);
console.log(persona1.calle);
```

### Asignar valores a las propiedades

**Es posible usar las dos formas de acceder a las propiedades para asignar nuevos valores a los datos almacenados en la propiedades del objeto.**

```javascript
const persona1 = { nombre: "Homero",
                   edad: 39,
                   calle: "Av. Siempreviva 742"};
                   
persona1["nombre"] = "Marge";
persona1.edad = 36;
```

### Constructores

En JS, el constructor de un objeto es **una función que usamos para crear un nuevo objeto cada vez que sea necesario. Con esta “función constructora” podemos inicializar las propiedades del objeto al momento de ser instanciado con NEW.**

```javascript
function Persona(nombre, edad, calle) {
    this.nombre = nombre;
    this.edad 	 = edad;
    this.calle  = calle;
}
const persona1 = new Persona("Homero", 39, "Av. Siempreviva 742");
const persona2 = new Persona("Marge", 36, "Av. Siempreviva 742");
```

### Constructor y NEW

En el ejemplo anterior, se define la función Persona, donde se asignan las diferentes propiedades con los valores recibidos como parámetros.

Luego, en algún lugar del código posterior a esas líneas, **se puede construir un objeto Persona, declarando una variable y asignando la referencia del objeto instanciado mediante la instrucción new Persona**(...)

### Uso del THIS

**La palabra clave this (“este”) refiere al elemento actual en el que se está escribiendo el código.**  Cuando se emplea un función constructora para crear un objeto (con la palabra clave new), this está enlazado al nuevo objeto instanciado.
**This es muy útil para asegurar que se emplean las propiedades del objeto actual.**

 ```javascript
 function Persona(literal) {
    this.nombre = literal.nombre;
    this.edad   = literal.edad;
    this.calle  = literal.calle;
}
const persona1 = new Persona({ nombre: "Homero", edad: 39, calle: "Av.Siempreviva 742" });
```

### Metodo <> Función

Como vimos anteriormente, las funciones en JS se pueden definir en cualquier parte del código, y pueden ser llamadas desde cualquier otra parte del código posterior.
**Los métodos de los objetos, también son técnicamente funciones, sólo que se limitan a poder ser ejecutados únicamente desde el mismo objeto.**

#### Función

```javascript
//Funciones: Generalmente retornar un valor y son de acceso global.
function f1(){
    return this;
}
```

#### Método

```javascript
//Métodos: Se requiere un objeto y puede no retornar un valor.
function Persona(nombre, edad, calle) {
    this.nombre = nombre;
    this.edad = edad;
    this.calle = calle;
}
```

### Métodos de objetos en JavaScript

JavaScript cuenta con sus propios objetos, incluso ya usamos algunos de ellos sin identificar que son objeto.
Por ejemplo: Cada vez que creamos una cadena de caracteres se crea automáticamente como una instancia del objeto String, y por lo tanto tiene varios métodos/propiedades comunes disponibles en ella.

```javascript
let cadena = "HOLA CODER";
//Propiedad de objeto String: Largo de la cadena.
console.log(cadena.length);
//Método de objeto String: Pasar a minúscula.
console.log(cadena.toLowerCase());
//Método de objeto String: Pasar a mayúscula.
console.log(cadena.toUpperCase());
```

### Métodos personalizados
**Podemos crear nuestro propios métodos para objetos personalizados, referenciando funciones por su nombre o definiendo funciones anónimas asociadas a una propiedad de la función constructora**. 
Llamar a un método es similar a acceder a una propiedad, pero se agrega () al final del nombre del método, posiblemente con argumentos.

```javascript
function Persona(nombre, edad, calle) {
    this.nombre = nombre;
    this.edad   = edad;
    this.calle  = calle;
    this.hablar = function(){ console.log("HOLA SOY "+ this.nombre)}
}
const persona1 = new Persona("Homero", 39, "Av. Siempreviva 742");
const persona2 = new Persona("Marge", 36, "Av. Siempreviva 742");
persona1.hablar();
persona2.hablar();
```

### Operador IN y FOR..IN

**El operador IN devuelve TRUE si la propiedad especificada existe en el objeto.** 
Mientra que el bucle for...in permite acceder a todas las propiedades del objeto, obteniendo una propiedad por cada iteración.

```javascript
const persona1 = { nombre: "Homero", edad: 39, calle: "Av. Siempreviva 742"};
//devuelve true porque la clave "nombre" existe en el objeto persona1
console.log( "nombre" in persona1);
//devuelve false porque la clave "origen" no existe en el objeto persona1
console.log( "origen" in persona1);
//recorremos todas las propiedades del objeto con el ciclo for...in
for (const propiedad in persona1) {
    console.log(persona1[propiedad]);
}
```

## Clases

Las clases de javascript, introducidas en ES6, proveen una sintaxis **mucho más clara y simple para crear objetos personalizados**.
**Son una equivalencia al empleo de función constructora** y permite definir distintos tipo de métodos. 

```javascript
class Persona{
    constructor(nombre, edad, calle) {
        this.nombre = nombre;
        this.edad   = edad;
        this.calle  = calle;
    }
}
const persona1 = new Persona("Homero", 39, "Av. Siempreviva 742");
```

### Clases y métodos

En la declaración de clase, la función constructora es reemplaza por el método **constructor**. Los métodos en las clases no referencian a propiedades, se declaran dentro del bloque sin la palabra function

```javascript
class Persona{
    constructor(nombre, edad, calle) {
        this.nombre = nombre;
        this.edad   = edad;
        this.calle  = calle;
    }
    hablar(){
        console.log("HOLA SOY "+ this.nombre);
    }
}
const persona1 = new Persona("Homero", 39, "Av. Siempreviva 742");
persona1.hablar();
```

#### Ejemplo:

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
    vender() {
        this.vendido = true;
    }
}
const producto1 = new Producto("arroz", "125");
const producto2 = new Producto("fideo", "50");
producto1.sumaIva();
producto2.sumaIva();
producto1.vender();
```


