---
tags: [Coderhouse, JavaScript]
title: '[JavaScript Clase 11] JQuery, selectores y eventos'
created: '2021-07-20T04:40:34.476Z'
modified: '2021-08-05T14:36:05.110Z'
---

# [JavaScript Clase 11] JQuery, selectores y eventos

jQuery nos brinda un conjunto de **métodos para asociar eventos a un selector**.  Son una equivalencia al empleo de addeventlistener y se prefieren si estamos usando la librería para acceder al DOM.
También tenemos una serie de métodos atajo (shortcut) para asociar los eventos de forma más sencilla.

## $(document).ready()

El método ready() de jQuery **se emplea para detectar que el DOM está listo para usarse**. Cuando un página se está cargando existe un tiempo de espera hasta que podemos manipular el DOM. Usamos este evento para asegurarnos que podemos acceder a los elementos HTML en el momento oportuno, luego de ser detectados por el cliente.
Es el equivalente al evento nativo de JavaScript DOMContentLoaded 

```javascript
$( document ).ready(function() 
{
   console.log( "El DOM esta listo" );
});
```

### Forma corta de ready()

La forma recomendada de declarar el método ready() es utilizando la asociación explícita a document. Pero existe una forma corta de definición y dado que el manejador de eventos generalmente es una función anónima, es posible usar funciones flechas.

```javascript
//Forma explicita
$(document).ready(function() {
    console.log('El DOM esta listo');
});
//Forma corta de ready()
$(function() {
    console.log('El DOM esta listo');
});
//Forma corta con arrow function
$(() => {
    console.log('El DOM esta listo');
});
```

### Ventajas de $(document).ready()

- A diferencia del evento load, no espera a que se carguen todas las imágenes y recursos externo en la ventana para ejecutarse.
- Permite detectar cuando el DOM está cargado en el browser para efectuar cambios inmediatos sobre la estructura HTML, sin errores.
- Se puede escribir múltiples funciones ready(), ejecutándose en el orden que sea definen cuando el DOM está listo. Pudiendo separar la respuesta al evento en más de un manejador de eventos.

ready() VS load()

Si es necesario determinar cuando se cargaron todas las imágenes y otros recursos externos de la página usamos el evento load. **El evento ready ocurre antes que load**.
En cualquier llamado, puedes reemplazar el caracter $ por jQuery.  Es indistinto.

```javascript
$( document ).ready(function() {
    console.log('El DOM esta listo');
});

window.addEventListener('load', function() {
    console.log( 'Todos los elementos de la ventana están cargados' );
});
```

## Método ON

Con el método on() podemos asignar eventos a elementos del DOM. 
Es una opción al método addEventListener() de JS Vanilla cuando usamos jQuery

```javascript
//Agregamos un botón al body como primer elemento
$('body').prepend('<button id="btnjQuery">CLICK</button>');
//Asociamos el evento click al botón creado
on('click', function () {
    console.log("Respuesta a un click");
});
$('#btnjQuery').//Asociamos el evento doble click al botón creado
$('#btnjQuery').on('dblclick', () => {
    console.log("Respuesta al doble click");
});
```

### Ejemplo aplicado: asociar evento a boton creado

```javascript
// Array de objetos para agregar información al DOM.
const productos = [{ id: 1,  nombre: "Arroz", precio: 125 },
{  id: 2,  nombre: "Fideo", precio: 70 },
{  id: 3,  nombre: "Pan"  , precio: 50},
{  id: 4,  nombre: "Flan" , precio: 100}];
// Recorremos el array con for..of
for (const producto of productos) {
    //Por cada producto además de los datos agregamos un botón 
    $("#app").append(`<div>
                        <h4>  Producto: ${producto.nombre}</h4>
                        <b> $ ${producto.precio}</b>
                        <button id="btn${producto.id}">Comprar</button>
                        </div>`);
    //Asociamos el evento a botón recién creado.
    $(`#btn${producto.id}`).on('click', function () {
        console.log(`Compreaste ${producto.nombre}`);
    });
}
```

## Métodos SHORCUT

## click()

Este método click() es un atajo para .on("click", manejador). El evento click se dispara cuando el puntero del ratón está sobre el elemento, y el botón del ratón se presiona y se suelta. Cualquier elemento HTML puede recibir este evento.

```javascript
//Agregamos dos botones con jQuery
$("body").prepend('<button id="btn1">BUTTON</button>');
$("body").prepend('<button id="btn2">BUTTON</button>');
//Asociamos el evento click para btn1
$("#btn1").click(function () { 
    console.log(this);
});
//Evento click para btn2 con Arrow function y parámetro e
$("#btn2").click((e) => { 
    console.log(e.target);
});
```

### change()

Este método change() es un atajo para .on( "change", manejador ).  El evento change se dispara cuando el valor del elemento cambia. Este evento está limitado a los elementos de html input>, textarea> y select>.

```javascript
//Agregamos inputs con jQuery
$("body").prepend(`<input type="text"   class="inputsClass">
                   <input type="number" class="inputsClass">
                   <select class="inputsClass">
                        <option value="1" selected >ID 1</option>
                        <option value="2">ID 2</option>
                        <option value="3">ID 3</option>
                    </select>`);
//Asociamos el evento change a todos los inputs
$(".inputsClass").change(function (e) { 
    console.log(e.target.value);
    console.log(this.value);
});
```

### submit()

Este método submit() es un atajo para .on( "submit", manejador ). 
El evento submit se dispara cuando el usuario envía un formulario. Sólo disponible para elementos <form>.

```javascript
//Agregamos un formulario con jQuery
$("body").prepend(`<form id="myForm">
                       <input type="text"  >
                       <input type="number">
                       <input type="submit">
                   </form>`);
//Asociamos el evento submit al formulario
$("#myForm").submit(function (e) {
    //Prevenimos el comportamiento de submit 
    e.preventDefault();
    //Obtenemos hijos del formulario
    let hijos = $(e.target).children();
    //Primer input type="text"
    console.log(hijos[0].value);
    //Primer input type="number"
    console.log(hijos[1].value);
});
```

## Método TRIGGER

El método trigger() dispara un evento específico y el comportamiento predeterminado de un evento (como el envío de formularios) para los elementos seleccionados. Se usa para activar eventos de otros elementos.

```javascript
//Agregamos un botón y un input
$("body").prepend('<button id="btn1">BUTTON</button>');
$("body").prepend('<input  id="ipt1" type="text">');
//Asociamos el evento change al ipt1
$("#ipt1").change((e) => { 
    alert("El valor es " + e.target.value);
});
//Asociamos el evento click para btn1 y usamos trigger
$("#btn1").click(() => { 
    //Usamos trigger para disparar el evento change de ipt1 
    $("#ipt1").trigger("change");
});
```

### Ejemplo aplicado: input hidden

```javascript
// Array de objetos para agregar información al DOM.
const productos = [{ id: 1,  nombre: "Arroz", precio: 125 },
{  id: 2,  nombre: "Fideo", precio: 70 },
{  id: 3,  nombre: "Pan"  , precio: 50},
{  id: 4,  nombre: "Flan" , precio: 100}];
// Asociamos el evento click en ready luego del DOM Generado
$(document).ready(function () {
    $(".btnComprar").click(function (e) { 
        //Obtenemos hijos del padre <div> desde el target
        let hijos = $(e.target).parent().children();
        //Primer input, valor de ID oculto
        console.log(hijos[0].value);
    });
});
// Recorremos el array con for..of
for (const producto of productos) {
    //Por cada producto además de los datos agregamos un botón 
    $("#app").append(`<div>
                        <input value="${producto.id}" type="hidden">
                        <h4>  Producto: ${producto.nombre}</h4>
                        <b> $ ${producto.precio}</b>
                        <button class="btnComprar">Comprar</button>
                    </div>`);
}
```

Código de clase

```javascript
//JQUery selectores y eventos
$(document).ready(function() {
    console.log("Cargado el DOM");
});

$(window).on('load', function() {
    console.log("Se cargó todo incluyendo imagenes y archivos externos");
});

function validarCampos() {
    if (($("#usu").val().toLowerCase() == "pepe") && ($("#pass").val() == "12345")) {
        $("#saludo").html("Welcome " + $("#usu").val());
    } else {
        alert("DATOS ERRONEOS");
    }
}

//ACCION DEL BOTON VALIDAR
$("#botonValidar").on('click', validarCampos);
//ALTERNATIVA
//$("#botonValidar").click(validarCampos);

//Diapo18
// Array de objetos para agregar información al DOM.
/*const productos = [{ id: 1, nombre: "Arroz", precio: 125 },
    { id: 2, nombre: "Fideo", precio: 70 },
    { id: 3, nombre: "Pan", precio: 50 },
    { id: 4, nombre: "Flan", precio: 100 }
];
let carrito = [];
// Recorremos el array con for..of
for (const producto of productos) {
    //Por cada producto además de los datos agregamos un botón 
    $("#app").append(`<div>
                        <h4>  Producto: ${producto.nombre}</h4>
                        <b> $ ${producto.precio}</b>
                        <button id="btn${producto.id}">Comprar</button>
                        </div>`);
    //Asociamos el evento a botón recién creado.
    $(`#btn${producto.id}`).on('click', function() {
        //console.log(`Compraste ${producto.nombre}`);
        carrito.push(productos[producto.id - 1]);
        console.log(carrito);
    });
}*/

//accion boton borrar ver
let visibilidad = true;
$("#botonBorrarVer").on('click', () => {
    //if ternario
    visibilidad ? $(".aRemover").css({ display: "none" }) : $(".aRemover").css({ display: "inline-block" });
    visibilidad = !visibilidad;
    console.log(visibilidad);
});

//trigger dispara otro evento previamente codificado
$(".inputs").keydown(() => {
    $("#botonBorrarVer").trigger('click');
});

//Diapo final
// Array de objetos para agregar información al DOM.
// const productos = [{ id: 1, nombre: "Arroz", precio: 125 },
//     { id: 2, nombre: "Fideo", precio: 70 },
//     { id: 3, nombre: "Pan", precio: 50 },
//     { id: 4, nombre: "Flan", precio: 100 }
// ];
// // Asociamos el evento click en ready luego del DOM Generado
// $(document).ready(function() {
//     $(".btnComprar").click(function(e) {
//         //Obtenemos hijos del padre <div> desde el target
//         let hijos = $(e.target).parent().children();
//         //Primer input, valor de ID oculto
//         console.log(hijos[0].value);
//     });
// });
// // Recorremos el array con for..of
// for (const producto of productos) {
//     //Por cada producto además de los datos agregamos un botón 
//     $("#app").append(`<div>
//                         <input value="${producto.id}" type="hidden">
//                         <h4>  Producto: ${producto.nombre}</h4>
//                         <b> $ ${producto.precio}</b>
//                         <button class="btnComprar">Comprar</button>
//                     </div>`);
// }

//EJEMPLO DIAPO MODIFICACION FINAL
// Array de objetos para agregar información al DOM.
const productos = [{ id: 1, nombre: "Arroz", precio: 125 },
    { id: 2, nombre: "Fideo", precio: 70 },
    { id: 3, nombre: "Pan", precio: 50 },
    { id: 4, nombre: "Flan", precio: 100 }
];

let carrito = [];
//funcion para agregar la propiedad cantidad al objeto literal para el carrito
function agregarItem(objeto) {
    console.log("Agregando objeto:");
    Object.defineProperty(objeto, 'cant', { value: 1, writable: true });
    carrito.push(objeto);
}

// Recorremos el array con for..of
for (const producto of productos) {
    //Por cada producto además de los datos agregamos un botón 
    $("#app").append(`<div class="col-md-3">
                        <h4>  Producto: ${producto.nombre}</h4>
                        <b> $ ${producto.precio}</b>
                        <button class="btn btn-danger" id="btn${producto.id}">Comprar</button>
                        </div>`);
    //Asociamos el evento a botón recién creado.
    $(`#btn${producto.id}`).on('click', function() {
        console.log(`Compraste ${producto.nombre}`);
        //modificiacion
        //find con funcion flecha y desestructuración
        let objetoBuscado = carrito.find(({ id }) => id == producto.id);
        //undefined si no lo encuentra
        console.log("El objeto:");
        console.log(objetoBuscado);
        //if ternario
        (objetoBuscado != undefined) ? objetoBuscado.cant++: agregarItem(productos[producto.id - 1]);
        console.log("Carrito:");
        console.log(carrito);
    });
}
```

