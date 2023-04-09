---
tags: [Coderhouse, JavaScript]
title: '[JavaScript Clase 4] Funciones'
created: '2021-06-22T20:54:17.582Z'
modified: '2021-07-13T23:12:24.336Z'
---

# [JavaScript Clase 4] Funciones

## Funciones

Cuando se desarrolla una aplicación o sitio web, **es muy habitual utilizar una y otra vez las mismas instrucciones**.
En programación, una función es un conjunto de instrucciones que se agrupan para realizar una tarea concreta, que luego se pueden reutilizar a lo largo de diferentes instancias del código.

## Sintaxis

Todas las funciones se escriben igual. Deben tener un nombre en minúscula y sin espacios. Deben abrirse y cerrase con llaves. El contenido de la función se escribe entre las llaves.  El nombre de la función no se puede repetir en otra.

```javascript
function saludar() {
    console.log("¡Hola estudiantes!");
}

```

Una vez que declaramos la función podemos usarla en cualquier otra parte del código las veces que queramos. 
Para ejecutar una función sólo hay que escribir su nombre y finalizar la sentencia con (). A esto se lo conoce como llamada de la función

```javascript
saludar();
```

### Ejemplo:

```javascript
function solicitarNombre(){
    let nombreIngresado   = prompt("Ingresar nombre");
    alert("El nombre ingresado es " + nombreIngresado);
} 
```

Para llamar a la función, la invocamos en otra parte del código:

```javascript
solicitarNombre() ;
} 
```

## Parámetros

Una función simple, puede no necesitar ninguna dato para funcionar. 
Pero cuando empezamos a codificar funciones más complejas, nos encontramos con la necesidad de recibir cierta información para funcionar. 
Cuando enviamos a la función uno o más valores para que ser empleados en sus operaciones, estamos hablando de los parámetros de la función.
Los parámetros se envían a la función mediante variables y se colocan entre los paréntesis posteriores al nombre de la función.

```javascript
function conParametros(parametro1, parametro2) {
    console.log(parametro1 + " " + parametro2);
}
```

Dentro de la función, el valor de la variable parametro1 tomará al primer valor que se le pase a la función, y el valor de la variable parametro2 tomará el segundo valor que se le pasa.

### Ejemplo

```javascript
//Declaración de variable para guardar el resultado de la suma
let resultado = 0;
//Función que suma dos números y asigna a resultado
function sumar(primerNumero, segundoNumero) {
    resultado = primerNumero + segundoNumero;
}
//Función que muestra resultado por consola
function mostrar(mensaje) {
    console.log(mensaje);
}
//Llamamos primero a sumar y luego a mostrar
sumar(6, 3);            
mostrar(resultado); 
```

## Return

El ejemplo anterior sumamos dos números a una variable declarada anteriormente. Pero las funciones pueden generar un valor de retorno usando la palabra return, obteniendo el valor cuando la función es llamada

```javascript
function sumar(primerNumero, segundoNumero) {
    return primerNumero + segundoNumero;
}
let resultado = sumar(5, 8);
```

## Variables locales y globales

El ámbito de una variable (llamado **"scope"** en inglés), es la zona del programa en la que se define la variable, el **contexto** al que pertenece la misma dentro de un algoritmo.

JavaScript define dos ámbitos para las variables: **global y local.**

### Variables locales

Cuando definimos una variable dentro de una función o bloque es una variable local, **la misma existirá sólamente durante la ejecución de esa sección**. Si queremos utilizarla por fuera, la variable no existirá para JS.

### Variables globales

**Si una variable se declara fuera de cualquier función o bloque, automáticamente se transforma en variable global,** independientemente de si se define utilizando la palabra reservada var, o no.

## Funciones anónimas

Una función **anónima es una función que se define sin nombre y se utiliza para ser pasadas como parámetros o asignada a variable**. En el caso de asignarla a una variable, pueden llamar usando el identificador de la variable declarada

```javascript
//Generalmente, las funciones anónimas se asignan a variables declaradas como constantes
const suma  = function (a, b) { return a + b };
const resta = function (a, b) { return a - b };
console.log(suma(15,20));
console.log(resta(15,5));
```

## Funciones flecha

Identificamos a las funciones flechas como **funciones anónimas de sintaxis simplificada**.Están disponibles desde la versión ES6 de JavaScript, no usan la palabra function pero usamos => (flecha) entre los parámetros y el bloque

```javascript
const suma  = (a, b) => { return a + b };
//Si es una función de una sola línea con retorno podemos evitar escribir el cuerpo.
const resta = (a, b) =>  a - b ;
console.log(suma(15,20));
console.log(resta(20,5));
```

### Ejemplo

```javascript
const suma  = (a,b) => a + b;
const resta = (a,b) => a - b;
//Si una función es una sola línea con retorno y un parámetro puede evitar escribir los ()
const iva   = x => x * 0.21;
let precioProducto  = 500; 
let precioDescuento = 50;  
//Calculo el precioProducto + IVA - precioDescueto
let nuevoPrecio = resta(suma(precioProducto, iva(precioProducto)), precioDescuento); 
console.log(nuevoPrecio);
```



