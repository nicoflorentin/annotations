---
tags: [Coderhouse, JavaScript]
title: '[JavaScript Clase 10] JQuery y selectores'
created: '2021-07-08T21:50:57.704Z'
modified: '2021-08-05T14:36:07.149Z'
---

# [JavaScript Clase 10] JQuery y selectores

## Qué es JQuery?

jQuery es una librería que **sirve para manipular el DOM, controlar eventos, agregar animaciones y ejecutar llamadas AJAX**, entre otras cosas.
Si bien ya vimos el uso del DOM mediante las herramientas nativas de JS, lo que diferencia a **jQuery es que resulta más práctico y potente**, además de estar más sistematizado y ordenado desde la forma en que está desarrollado.

## JQuery en la actualidad

En la actualidad **existen opciones más modernas que jQuery que proveen las mismas  funcionalidades** que esta librería. (Incluso en las últimas versiones de JS)
Pero su presencia en el mercado es aún significativa y existe un conjunto de tecnología en producción dependiente de esta librería, lo que la transforma en una excelente candidata a ofertas laborales en migración de sistemas.

- JQuery utiliza los mismos selectores de CSS3 para operar sobre los elementos.
- Diseño y estructura ordenada.
- Es open source.
- Rapidez para ejecutar y operar sobre el DOM.
- Compatibilidad con muchos plugins. (animaciones, sliders, componentes, etcétera).
- Facil de aprender. (4 Clases)

### Cargar con URL

Basta con localizar una URL de un CDN que provea la librería jQuery y cargarlo en el archivo HTML. 
Una vez que localizamos la URL del archivo, la referenciamos en nuestro archivo HTML antes de cerrar el </body> 

```html
<script src="https://code.jquery.com/jquery-3.5.1.min.js"></script>
```

### Cargar localmente

Para usarlo localmente, debemos descargar el archivo .js de la página oficial de jQuery, y luego incluirlo en nuestra carpeta del proyecto.
Finalmente, cargamos el script en el archivo html **antes de cerrar el body**

```html
<script src="js/jquery-3.5.1.min.js"></script>
```

### Selectores en JQuery

El concepto de selector es tal vez el mayor logro que introdujo jQuery. **Se refiere a la forma de identificar a los diferentes elementos del DOM y poder operar sobre ellos**. 
En vez de emplear los métodos getElementById(), getElementsByClassName() y  getElementsByTagName() de document, **con JQuery podemos usar un único medio para acceder al DOM**. 

### Usando selectores

```javascript
// Acceso equivalente: document.getElementById("listaPaises");
$("#listaPaises");
// Acceso equivalente: document.getElementsByClassName("paises")
$(".paises");
// Acceso equivalente: document.getElementsByTagName("li")
$("li");
```

### Combinación de selectores

```javascript
$( "div" ); 	//selecciona todos los <div> de la página
$( "a" );		//selecciona todos los <a>
$( "p, a" ); 	//seleccionar todas los los <p>, y los <a>
$( "li.nombre-clase #caja" ); 
//seleccionar todo <li> con clase "nombre-clase", y que tengan un hijo con ID "caja"
```

### Selectores avanzados

```javascript
$( "p:last" ); 				//Selecciona el último <p> de la página
$( "li:first-child" ); 		//Selecciona todos los <li> que son primeros hijos
$( "li:last-child" ); 		//Selecciona todos los <li> que son últimos hijos
$( "li:only-child" ); 		//Selecciona todos los <li> que sean hijos únicos
$( "li:nth-child(3)" ); 		//Selecciona todos los <li> que sean el 3er elemento 
$( "tr:nth-child(odd)" ); 	//Selecciona todos los <tr> que sean impares
$( "tr:nth-child(even)" ); 	//Selecciona todos los <tr> que sean pares
$( "div:nth-child(3n)" ); 	//Selecciona cada tercer elemento <div>
```

### Selectores para formularios

```javascript
$( ":text" );
$( ":checkbox" );
$( ":radio" );
$( ":image" );
$( ":submit" );
$( ":reset" );
$( ":password" );
$( ":file" );
$( ":input" ); 	//Selecciona los elementos input, textarea,select y button
$( ":button" ); 	//Selecciona los elementos button e input con atributo "type"="button"
$( ":enabled" );	//Selecciona los elementos del formulario activados
$( ":disabled" ); 	//Selecciona los elementos del formulario desactivados
$( ":checked" ); 	//Selecciona los radio buttons y checkboxes que están pulsados
$( ":selected" ); 	//Elementos de una lista de opciones que este seleccionados
```

## Agregar elementos con JQuery

Una vez obtenido un el elemento del HTML con el selector **es posible agregar a un nuevo elemento al DOM**.
En jQuery no es necesario crear un nodo del tipo de etiqueta con createElement(). Podemos **agregar inmediatamente la estructura HTML deseada** con los métodos de la librería append() y prepend()

```javascript
/* El siguiente código es la equivalencia de creación en JS Vanilla
var parrafo = document.createElement("p");
parrafo.innerHTML = "<h2>¡Hola Coder!</h2>"; 
document.body.appendChild(parrafo)
*/
$('body').append("<p><h2>¡Hola Coder!</h2></p>");
```

### JQuery **append()**

El método .append() inserta el contenido especificado como **último hijo del elemento seleccionado**.

```javascript
let producto   = { id: 1,  nombre: "Arroz", precio: 125 };
//Es posible usar plantillas de texto en el parámetro.
$("#app").append(`<div><h3> ID: ${producto.id}</h3>
                  <p>  Producto: ${producto.nombre}</p>
                  <b> $ ${producto.precio}</b></div>`);
```

### JQuery **prepend()**

El método .prepend() inserta el contenido especificado como **primer hijo del elemento seleccionado**.

```javascript
let producto2   = { id: 2,  nombre: "Flan", precio: 150 };
//Es posible usar plantillas de texto en el parámetro.
$("#app").prepend(`<div><h3> ID: ${producto2.id}</h3>
                 <p>  Producto: ${producto2.nombre}</p>
                 <b> $ ${producto2.precio}</b></div>`);
```

#### Ejemplo aplicado

```javascript
const productos = [{ id: 1,  nombre: "Arroz", precio: 125 },
{  id: 2,  nombre: "Fideo", precio: 70 },
{  id: 3,  nombre: "Pan"  , precio: 50},
{  id: 4,  nombre: "Flan" , precio: 100}];

for (const producto of productos) {
    $("#app").append(`<div><h3> ID: ${producto.id}</h3>
    <p>  Producto: ${producto.nombre}</p>
    <b> $ ${producto.precio}</b></div>`);
}
```

Código de clase

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <!-- CSS only -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-+0n0xVW2eSR5OomGNYDnhzAbDsOXxcvSN1TPprVMTNDbiYZCxYbOOl7+AMvyTG2x" crossorigin="anonymous">
    <title>Clase 11</title>
</head>

<body>
    <div class="container">
        <div id="fila_prueba" class="row" style="background-color:#aaa">
            <div class="col">
                <h1 class="text-center">Librerías y JQuery</h1>
            </div>
        </div>
        <div class="row" style="background-color:rgb(112, 133, 145)">
            <div class="col-sm">
                Columna 1
            </div>
            <div class="col-sm">
                Columna 2
            </div>
            <div class="col-sm">
                Columna 3
            </div>
        </div>
        <div>
            <ul class="milista list-group list-group-horizontal">
                <!-- Aqui los productos -->
            </ul>
        </div>
    </div>
    <!-- JavaScript Bundle with Popper -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.1/dist/js/bootstrap.bundle.min.js" integrity="sha384-gtEjrD/SeCtmISkJkNUaaKMoLD0//ElJ19smozuHV6z3Iehds+3Ulb9Bn9Plx0x4" crossorigin="anonymous"></script>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js" integrity="sha256-/xUj+3OJU5yExlq6GSYGSHk7tPXikynS7ogEvDej/m4=" crossorigin="anonymous"></script>
    <script src="script.js"></script>
</body>

</html>
```

```javascript
//jquery
$("#fila_prueba").css({ background: 'red', color: 'white' });
//js puro
//document.getElementById("fila_prueba").style.background = "red";
//document.getElementById("fila_prueba").style.color = "white";

//append
$("body").append("<p>Hola camada 14470 !!!</p>");
//prepend
$(".container").prepend("<button class='btn btn-warning'>Boton Prueba</button>");

//diapo modificada
const productos = [{ id: 1, nombre: "Arroz", precio: 125 },
    { id: 2, nombre: "Fideo", precio: 70 },
    { id: 3, nombre: "Pan", precio: 50 },
    { id: 4, nombre: "Flan", precio: 100 }
];

for (const producto of productos) {
    $(".milista").append(`<li class="list-group-item"><h3> ID: ${producto.id}</h3>
    <p>  Producto: ${producto.nombre}</p>
    <b> $ ${producto.precio}</b></div>`);
}
```


