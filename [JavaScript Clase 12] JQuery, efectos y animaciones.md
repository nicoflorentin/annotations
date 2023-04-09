---
tags: [Coderhouse, JavaScript]
title: '[JavaScript Clase 12] JQuery, efectos y animaciones'
created: '2021-07-22T02:10:34.097Z'
modified: '2021-08-08T18:05:06.546Z'
---

# [JavaScript Clase 12] JQuery, efectos y animaciones

JQuery provee métodos para incorporar efectos y animaciones a los elementos del DOM.
El objetivo es combinar las diferentes variantes entre sí para darle a una web o app dinamismo y movimiento.

### show

El método show()muestra un elemento del DOM. **Suponiendo que se encuentre oculto mediante css (display:none)**, al seleccionarlo con JQuery y ejecutar show(), el elemento aparecerá en la pantalla.

```javascript
//Agregemos <h3> con jQuery ocultos con  style="display: none;"
$("body").prepend('<h3  style="display: none" >¡Hola Coder1!</h3>');
$("body").prepend('<h3  style="display: none" >¡Hola Coder2!</h3>');
//Mostramos con show() todos los <h3>
$("h3").show();
```

### hide

El método hide() **es la inversa a show**. Suponiendo que se encuentre visible mediante css, al seleccionarlo con JQuery y ejecutar hide(), el elemento **desaparecerá** de la pantalla.

```javascript
//Agregamos <h3> con jQuery
$("body").prepend('<h3>¡Hola Coder1!</h3>');
$("body").prepend('<h3>¡Hola Coder2!</h3>');
//Ocultamos con hide() todos los <h3>
$("h3").hide();
```

### fadeIn

El método fadeIn() tiene el mismo fin que la función show, solo que en este caso, **el elemento aparece con una transición**. Es decir, que al llamar fedeIn el elemento empieza a aparecer de forma gradual, hasta  que esté completamente visible.

```javascript
//Agreguemos <h3> con jQuery ocultos con  style="display: none;"
$("body").prepend('<h3  style="display: none" >¡Hola Coder1!</h3>');
$("body").prepend('<h3  style="display: none" >¡Hola Coder2!</h3>');
//Mostramos con fadeIn() todos los <h3>
$("h3").fadeIn();
```

### fadeOut

El método fadeOut()tiene el mismo fin que la función hide, solo que en este caso, **el elemento desaparece con una transición**. Es decir, que al llamar fedeOut el elemento empieza a desaparecer de forma gradual, hasta  que esté completamente invisible.

```javascript
//Agregemos <h3> con jQuery"
$("body").prepend('<h3>¡Hola Coder1!</h3>');
$("body").prepend('<h3>¡Hola Coder2!</h3>');
//Ocultamos con fadeOut() todos los <h3>
$("h3").fadeOut();
```

### Velocidad del fade

Tanto para fadeOut()como fadeIn() **se puede enviar un parámetro opcional para indicar la velocidad el fade**. Se puede usar la palabra "slow" o "fast", o también un número en milisegundos para indicar la duración total de la transición.

## Callback del fade

Tanto para fadeOut()como fadeIn() se le puede enviar un segundo parámetro opcional **para indicar una función que se ejecutará cuando la animación termine.**

```javascript
//Agregamos <h3> con jQuery
$("body").prepend('<h3>¡Hola Coder1!</h3>');
//Ocultamos con fadeOut() todos los <h3>
$("h3").fadeOut("slow", function(){
    //Cuando termina de ocultarse el elemento lo mostramos nuevamente
    $("h3").fadeIn(1000);
}); 
```

### slideDown

```javascript
//Agregamos un botón y un div con jQuery
$("body").prepend('<button id="btn1">Mostrar</button>');
$("body").prepend(`<div id="div1" style="height: 120px">
                        <h3>¡Hola Coder!</h3>
                        <h4>Sorpresa 2</h4>
                    </div>`);
//Usamos slideDown sobre div1 en respuesta al click del boton btn1
$("#btn1").click(() => { 
    $("#div1").slideDown("fast");
});
```

### slideUp

El método slideUp() **hace desaparecer al elemento haciendo una transición hacia arriba**. Es una alternativa al fadeOut. Se puede enviar los mismos parámetros de velocidad y callback que en fadeIn y fadeOut.

```javascript
//Agregamos un botón y un div con jQuery
$("body").prepend('<button id="btn1">Mostrar</button>');
$("body").prepend(`<div id="div1" style="height: 120px">
                        <h3>¡Hola Coder!</h3>
                        <h4>Sorpresa 2</h4>
                    </div>`);
//Usamos slideUp sobre div1 en respuesta al click del boton btn1
$("#btn1").click(() => { 
    $("#div1").slideUp("fast");
});
```

### Slide Toggle

El método slideToggle() **hace aparecer o desaparecer el elemento mediante slide**. En función de que el elemento esté visible o no, ejecuta slideUp, o slideDown.

```javascript
//Agregamos un botón y un div con jQuery
$("body").prepend('<button id="btn1">Mostrar</button>');
$("body").prepend(`<div id="div1" style="height: 120px">
                        <h3>¡Hola Coder!</h3>
                        <h4>Sorpresa</h4>
                    </div>`);
//Usamos toggle sobre div1 en respuesta al click del botòn btn1
$("#btn1").click(() => { 
    $("#div1").toggle("fast");
});
```

## Modificar CSS con jQuery

JQuery provee un método para **aplicar cambios directos sobre el css del elemento**. Llamando a css() podemos indicar la propiedad a modificar del elemento seleccionado.
 La sintaxis funciona así:  selector.css("propiedad-css","valor");

```javascript
//Agregamos un parrafo con jQuery
$("body").prepend('<p class="titulo">Code House</p>');
//Modificamos las reglas CSS desde jQuery
$("p").css("background-color", "yellow");
$("p").css("width", "50%");
$(".titulo").css({  "color": "#ccc", 
                    "font-size": "40px", 
                    "borderLeft": "5px solid #ccc" });
```

### Método animate

El método animate() **nos permite crear efectos de animación sobre cualquier propiedad CSS numérica**. Se requiere como parámetro un objeto de propiedades CSS. Este objeto es similar al que se puede enviar al método .css(), salvo que el rango de propiedades es más restrictivo.

```javascript
//Agregamos un parrafo con jQuery
$("body").prepend('<p class="titulo">Code House</p>');
//Animamos sus propiedades CSS con animate
$(".titulo").animate({  left:'250px',
                        opacity:'0.5',
                        height:'150px',
                        width:'150px'   }, //1er parámetro propiedades
                        "slow",            //2do parámetro duración 
                        function(){        //3er parámetro callback
                            console.log("final de animación");
                        });
```

### Ejemplo aplicado (scroll animado)

```javascript
//Agregamos una estructura con jQuery
$("body").prepend(`</div>
                        <a>Ir a contacto</a>
                        <p style="height: 800px"></p>
                        <section id="seccionContacto">
                           <h4>¡Somos Coders!</h4>
                        </section>
                   </div>`);
// Asociamos la animación al click en un elemento <a>
$('a').click( function(e) { 
    e.preventDefault();
    //Animamos sus propiedades CSS con animate
    $('html, body').animate({
        scrollTop: $("#seccionContacto").offset().top  
    }, 2000);
} );
```

## Encadenar animaciones

Es posible encadenar métodos jQuery, lo cual permite definir una animación tras otra empleando en una única declaración.
Es recomendable emplear esta forma si es necesario **asociar múltiples animaciones consecutivas a un mismo elemento**. Para ahorrarnos consultas al DOM.

```javascript
//Agreguemos un párrafo con jQuery
$("body").prepend('<p id="p1">Coder House</p>');
//Declaración de métodos encadenados
$("#p1").css("color", "red")
        .slideUp(2000)
        .slideDown(2000);
```

### delay

El método delay() nos permite **retrasar la ejecución de comandos encadenados**. Puede utilizarse para establecer un tiempo de espera en milisegundos entre una animación y la siguiente.

```javascript
//Agregamos un párrafo con jQuery
$("body").prepend('<p id="p1">Coder House</p>');
//Declaración de métodos encadenados
$("#p1").css("color", "red")
        .slideUp(2000)
        .delay(2000)
        .slideDown(2000);
```

### Ejemplo aplicado (animando la compra)

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
        //Animaciòn de respuesta de compra
        $(e.target).parent().slideUp("slow");
    });
});
// Recorremos el array con for..of
for (const producto of productos) {
    //Por cada producto ademas de los datos agregamos un botón 
    $("#app").append(`<div>
                        <input value="${producto.id}" type="hidden">
                        <h4>  Producto: ${producto.nombre}</h4>
                        <b> $ ${producto.precio}</b>
                        <button class="btnComprar">Comprar</button>
                    </div>`);
}
```

## Código en clase

HTML

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <!-- CSS only -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-+0n0xVW2eSR5OomGNYDnhzAbDsOXxcvSN1TPprVMTNDbiYZCxYbOOl7+AMvyTG2x" crossorigin="anonymous">
    <title>Clase 13</title>
</head>

<body>
    <section>
        <button class="btn btn-danger" id="muestraParrafo">Mostrar Parrafo con FadeIn</button>
        <button class="btn btn-danger" id="ocultaParrafo">Ocultar Parrafo con FadeOut</button>
        <button class="btn btn-danger" id="slideImagen">Mostrar Imagen con SlideDown</button>
        <button class="btn btn-danger" id="slideImagenUp">Quitar Imagen con SlideUp</button>
        <button class="btn btn-danger" id="muestraOculta">Mostrar Imagen con FadeToggle</button>
    </section>
    <section>
        <p id="parrafo" style="display: none">Global settings Bootstrap sets basic global display, typography, and link styles. When more control is needed, check out the textual utility classes. Use a native font stack that selects the best font-family for each OS and device. For a more
            inclusive and accessible type scale, we use the browser’s default root font-size (typically 16px) so visitors can customize their browser defaults as needed. Use the $font-family-base, $font-size-base, and $line-height-base attributes as our
            typographic base applied to the body. Set the global link color via $link-color. Use $body-bg to set a background-color on the (#fff by default). These styles can be found within _reboot.scss, and the global variables are defined in _variables.scss.
            Make sure to set $font-size-base in rem.

        </p>
    </section>
    <section id=dinos>
        <image src=https://www.elpais.com.co/files/article_main/uploads/2017/01/30/588f7a4a917d8.jpeg></image>
    </section>
    <section id="dinos2">
        <image src=https://2.bp.blogspot.com/-PHUUy6pcmhU/V1Mq5w2joGI/AAAAAAAAH3c/ByRGYpWP-B4rcMnLsjj4S5-EeIIOIdNLgCLcB/s1600/dinosaurio.png></image>
    </section>
    <section id="app">
        <!-- Aqui productos -->
    </section>
    <!-- JavaScript Bundle with Popper -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.1/dist/js/bootstrap.bundle.min.js" integrity="sha384-gtEjrD/SeCtmISkJkNUaaKMoLD0//ElJ19smozuHV6z3Iehds+3Ulb9Bn9Plx0x4" crossorigin="anonymous"></script>
    <script src="https://code.jquery.com/jquery-3.5.0.js"></script>
    <script src="script.js"></script>
</body>

</html>
```

JAVASCRIPT

```javascript
//Jquery efectos y animaciones
$(document).ready(function() {
    $("#dinos").hide();
    $("#dinos2").hide();
});

$("#muestraParrafo").click(function() {
    $("#parrafo").fadeIn();
});
$("#ocultaParrafo").click(function() {
    $("#parrafo").fadeOut();
});

$("#muestraOculta").click(function() {
    $("#dinos2").fadeToggle(2000, function() {
        if ($("#muestraOculta").html() == "Mostrar Imagen con FadeToggle") {
            $("#muestraOculta").html("Ocultar Imagen con FadeToggle");
        } else {
            $("#muestraOculta").html("Mostrar Imagen con FadeToggle");
        }
        console.log("FadeToggle");
    });
});

$("#slideImagen").click(() => {
    $("#dinos").slideDown("slow");
});
$("#slideImagenUp").click(() => {
    $("#dinos").slideUp("slow");
});


//DIAPO 27 modificada
//Agregamos un parrafo con jQuery
$("body").prepend('<p class="titulo">Coder House</p>');
//Animamos sus propiedades CSS con animate
$(".titulo").animate({
        opacity: '0.5',
        height: '200px'
    }, //1er parámetro propiedades
    6000, //2do parámetro duración 
    function() { //3er parámetro callback
        console.log("final de animación");
    });

//Diapo 30
//Agregamos un párrafo con jQuery
$("body").append('<p id="p1">Coder House</p>');
//Declaración de métodos encadenados
$("#p1").css("color", "red")
    .delay(6000) //espera a que termine la otra animación
    .slideUp(2000)
    .slideDown(2000);

//Diapo 31
// Array de objetos para agregar información al DOM.
const productos = [{ id: 1, nombre: "Arroz", precio: 125 },
    { id: 2, nombre: "Fideo", precio: 70 },
    { id: 3, nombre: "Pan", precio: 50 },
    { id: 4, nombre: "Flan", precio: 100 }
];
// Asociamos el evento click en ready luego del DOM Generado
$(document).ready(function() {
    $(".btnComprar").click(function(e) {
        //Obtenemos hijos del padre <div> desde el target
        let hijos = $(e.target).parent().children();
        //Primer input, valor de ID oculto
        console.log(hijos[0].value);
        //Animaciòn de respuesta de compra
        $(e.target).parent().slideUp("slow");
    });
});
// Recorremos el array con for..of
for (const producto of productos) {
    //Por cada producto ademas de los datos agregamos un botón 
    $("#app").append(`<div>
                        <input value="${producto.id}" type="hidden">
                        <h4>  Producto: ${producto.nombre}</h4>
                        <b> $ ${producto.precio}</b>
                        <button class="btnComprar">Comprar</button>
                    </div>`);
}
```
