---
tags: [Coderhouse, JavaScript]
title: '[JavaScript Clase 1] JavaScript'
created: '2021-06-10T00:20:37.167Z'
modified: '2021-07-13T23:12:13.483Z'
---

#  [JavaScript Clase 1] JavaScript

JavaScript es un lenguaje de programación que se utiliza principalmente para aportar dinamismo a sitios y aplicaciones web.
Técnicamente, JavaScript es un lenguaje de programación interpretado por lo que el código escrito con JavaScript se puede probar directamente en cualquier navegador sin necesidad de procesos intermedios.
JavaScript funciona en complemento con los lenguajes web HTML Y CSS3.

**La primera versión de JavaScript ES1 se lanzó en 1997** y el lenguaje fue cambiando con el tiempo. En el curso nos focalizamos en las versiones ES5 y ES6.

### Cómo escribir JavaScript

JavaScript tiene sus propias reglas para la sintaxis, aunque respeta los estándares de muchos lenguajes de programación lógicos. Existen dos maneras de escribir código en JavaScript.
Dentro de un archivo html, entre medio de las etiquetas script
Ejemplo:

```html
<script>
    // Aquí se escribe el código JS 
</script>
```

En un archivo individual con extensión .js
Ejemplo: mi-archivo.js
Recuerda no utilizar espacios ni mayúsculas en los nombres de archivo. 

```html
<script src="js/main.js"></script>
```

## Sintaxis: Palabras reservadas

Palabras reservadas: son las palabras que se utilizan para construir las sentencias de JavaScript y que por tanto no pueden ser utilizadas libremente. 
Las palabras actualmente reservadas por JavaScript son: 

break, case, catch, continue, default, let, delete, do, else, finally, for, function, if, in, instanceof, new, return, switch, this, throw, try, typeof, var, void, while, with, etc.

## Variables y valores

Una variable es un espacio reservado en la memoria que, como su nombre indica, puede cambiar de contenido a lo largo de la ejecución de un programa. Podemos almacenar un número, un texto, un listado de números, etcétera. 

```html
<script>
    //Declaración de variable ES5. 
    var nombreVariable1;
  
    //Declaración de variable ES6.
    let   nombreVariable2;
    const LENGUAJE = "JAVASCRIPT";
  </script>
```

A una variable a la cual se le asigna un valor al declarar se le dice variable **inicializada**

## Prompt

La sentencia  **prompt**() mostrará un cuadro de diálogo para que el usuario ingrese un dato. Se puede proporcionar un mensaje que se colocará sobre el campo de texto. El valor que devuelve es una cadena que representa lo que el usuario ingresó.

``` html
<script>
    let nombreIngresado = prompt("Ingrese su nombre");
</script>
```

## Consola

La sentencia **console.log()** muestra el mensaje que pasemos como parámetro a la llamada en la consola JavaScript del Navegador web.

```html
<script>
    console.log("Mensaje de prueba");
</script>
```

## Alert

La sentencia **alert**() mostrará una ventana sobre la página web que estemos accediendo mostrando el mensaje que se pase como parámetro a la llamada.

```html
<script>
  alert("¡Hola Coder!");
</script>
```
