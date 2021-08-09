---
tags: [Coderhouse, JavaScript]
title: '[JavaScript Clase 8] DOM (Document Object Model)'
created: '2021-07-02T21:46:53.447Z'
modified: '2021-07-20T14:46:37.596Z'
---

# [JavaScript Clase 8] DOM (Document Object Model)

El Modelo de Objetos del Documento (DOM) **es una estructura de objetos generada por el navegador**, la cual representa la página HTML actual. Con JavaScript la empleamos para acceder y modificar de forma dinámica elementos de la interfaz.
Es decir que, por ejemplo, desde JS podemos modificar el texto contenido de una etiqueta **h1**

La estructura de un documento HTML son las etiquetas.
En el Modelo de Objetos del Documento (DOM), **cada etiqueta HTML es un objeto, al que podemos llamar nodo**. Las etiquetas anidadas son llamadas “nodos hijos” de la etiqueta “ nodo padre” que las contiene.
Todos estos objetos son accesibles empleando JavaScript mediante el objeto **global document**.
Por ejemplo, document.body es el nodo que representa la etiqueta **body**.

### Estructura del DOM

- **Cada etiqueta HTML se transforma en un nodo de tipo "Elemento"**. La conversión de etiquetas en nodos se realiza de forma jerárquica. 
- De esta forma, del nodo raíz solamente pueden derivar los nodos HEAD y BODY. 
- A partir de esta derivación inicial, cada etiqueta HTML se transforma en un nodo que deriva del correspondiente a su "etiqueta padre".
- La transformación de las etiquetas HTML habituales genera dos nodos: el primero es el nodo de tipo "Elemento" (correspondiente a la propia etiqueta XHTML) y el segundo es un nodo de tipo "Texto" que contiene el texto encerrado por esa etiqueta XHTML.

### Editar el DOM desde el navegador

Los navegadores modernos brindan medios para editar el DOM de cualquier página en tiempo real. Por ejemplo en Chrome podemos hacerlo mediante la Herramienta para desarrolladores en la pestaña “Elements”.
Si bien la estructura DOM está simplificada, es un medio muy útil para verificar y probar actualizaciones en la estructura.

#### Ejemplo:

```javascript
console.dir(document);
console.dir(document.head);
console.dir(document.body);
```

**El acceso a body usando la referencia document.body requiere que el script se incluya luego de <head> en el HTML**

```html
<body>
    <h2>Coder House</h2>
    <script src="js/main.js"></script>
  </body>
```

### Tipos de nodos

- La especificación completa de DOM define 12 tipos de nodos, aunque los más usados son:
- **Document**: Nodo raíz del que derivan todos los demás nodos del árbol.
- **Element**: Representa cada una de las etiquetas XHTML. Se trata del único nodo que puede contener atributos y el único del que pueden derivar otros nodos.
- **Attr**: Se define un nodo de este tipo para representar cada uno de los atributos de las etiquetas HTML, es decir, uno por cada par atributo=valor.
- **Text**: Nodo que contiene el texto encerrado por una etiqueta HTML.
- **Comment**: Representa los comentarios incluidos en la página HTML.

## Acceder a los nodos

Existen distintos métodos para acceder a los elementos del DOM empleando en la clase Document. Los más utilizados son:

### getElementById()

El método getElementById() sirve para acceder a un elemento de la estructura HTML, utilizando su **atributo ID como identificación**. 

```html
/CODIGO HTML DE REFERENCIA
<div id = "app">
<p id = "parrafo1" >Hola Mundo</p>
</div>
```

```javascript
//CODIGO JS
let div     = document.getElementById("app");
let parrafo = document.getElementById("parrafo1");
console.log(div.innerHTML);
console.log(parrafo.innerHTML);
```
### getElementsByClassName()

El método getElementsByClassName() sirve para acceder a un conjunto de elementos de la estructura HTML, **utilizando su atributo class como identificación**. Se retornará un Array de elementos con todas las coincidencias:

```html
//CODIGO HTML DE REFERENCIA
 <ul>
      <li class="paises">AR</li>
      <li class="paises">CL</li>
 	<li class="paises">UY</li>
 </ul>
```

 ```javascript
//CODIGO JS
let paises = document.getElementsByClassName("paises");
console.log(paises[0].innerHTML);
console.log(paises[1].innerHTML);
console.log(paises[2].innerHTML);
```

### getElementsByTagName()

El método getElementsByTagName() sirve para acceder a un conjunto de elementos de la estructura HTML, **utilizando su nombre de etiqueta como identificación**. Esta opción es la menos específica de todas, ya que es muy probable que las etiquetas se repitan en el código HTML.

```html
//CODIGO HTML DE REFERENCIA
<div>
<div>CONTENEDOR 2</div>
      <div>CONTENEDOR 3</div>
</div>
```

```javascript
//CODIGO JS
let contenedores = document.getElementsByTagName("div");
console.log(contenedores[0].innerHTML);
console.log(contenedores[1].innerHTML);
console.log(contenedores[2].innerHTML);
```

#### Ejemplo:

```javascript
let paises       = document.getElementsByClassName("paises");
let contenedores = document.getElementsByTagName("div");

for (const pais of paises) {
    console.log(pais.innerHTML);
}

for (const div of contenedores) {
    console.log(div.innerHTML);
}
```

## Agregar o quitar nodos

### Creación de elementos

Para crear elementos se utiliza la función **document.createElement()**, y se debe indicar el nombre de etiqueta HTML que representará ese elemento.
Luego debe agregarse como hijo el nodo creado con **appendChild()**, al body u a otro nodo del documento actual.

```javascript
// Crear nodo de tipo Elemento, etiqueta p
let parrafo = document.createElement("p");
// Insertar HTML interno
parrafo.innerHTML = "<h2>¡Hola Coder!</h2>"; 
// Añadir el nodo Element como hijo de body
document.body.appendChild(parrafo);
```

### Eliminar elementos

Se pueden eliminar nodos existentes y nuevos. El método **removeChild()** permite eliminar nodos hijos a cualquier nodo con tan sólo pasarle las referencias del nodo hijo [a] eliminar y su correspondiente padre:

```javascript
let parrafo      = document.getElementById("parrafo1");
//Elminando el propio elemento, referenciando al padre
parrafo.parentNode.removeChild(parrafo);

let paises       = document.getElementsByClassName("paises");
//Eliminando el primer elemento de clase paises
paises[0].parentNode.removeChild(paises[0])
```

### Obtener datos de inputs

Para obtener o modificar datos de un formulario HTML desde JS, podemos hacerlo mediante el DOM. **Accediendo a la propiedad value de cada input identificado con un ID**.

```html
//CODIGO HTML DE REFERENCIA
  <input id = "nombre" type="text">
  <input id = "edad"   type="number">
```

```javascript
//CODIGO JS
document.getElementById("nombre").value = "HOMERO";
document.getElementById("edad").value   = 39;

```

#### Ejemplo:

```javascript
//Obtenemos el nodo donde vamos a agregar los nuevos elementos
let padre      = document.getElementById("personas");
//Array con la información a agregar
let personas   = ["HOMERO","MARGE", "BART", "LISA","MAGGIE"];
//Iteramos el array con for...of
for (const persona of personas) {
    //Creamos un nodo <li> y agregamos al padre en cada ciclo
    let li = document.createElement("li");
    li.innerHTML = persona
    padre.appendChild(li);
}
```

## Plantillas de texto

### Plantillas literales

Al momento de incluir valores de las variables en una cadena de caracteres (string) empleábamos la concatenación. 
Esta forma puede ser poco legible ante un gran número de referencias. 

Un elemento incluido en JS ES6 que solventa esta situación son los **templates de literales**.

```javascript
let producto = { id: 1,  nombre: "Arroz", precio: 125 };
let concatenado = "ID : " + producto.id +" - Producto: " + producto.nombre + "$ "+producto.precio;
let plantilla   = `ID: ${producto.id} - Producto ${producto.nombre} $ ${producto.precio}`;
//El valor es idéntico pero la construcción de la plantilla es màs sencilla
console.log(concatenado);
console.log(plantilla);
```

### Plantillas literales e innerHTML

La plantillas son un medio para incluir variables en la estructura HTML de nodos nuevos o existentes , modificando el innerHTML

```javascript
let producto   = { id: 1,  nombre: "Arroz", precio: 125 };
let contenedor = document.createElement("div");
//Definimos el innerHTML del elemento con una plantilla de texto
contenedor.innerHTML = `<h3> ID: ${producto.id}</h3>
                        <p>  Producto: ${producto.nombre}</p>
                        <b> $ ${producto.precio}</b>`;
//Agregamos el contenedor creado al body
document.body.appendChild(contenedor);
```

#### Ejemplo:

```javascript
const productos = [{ id: 1,  nombre: "Arroz", precio: 125 },
                  {  id: 2,  nombre: "Fideo", precio: 70 },
                  {  id: 3,  nombre: "Pan"  , precio: 50},
                  {  id: 4,  nombre: "Flan" , precio: 100}];

for (const producto of productos) {
    let contenedor = document.createElement("div");
    //Definimos el innerHTML del elemento con una plantilla de texto
    contenedor.innerHTML = `<h3> ID: ${producto.id}</h3>
                            <p>  Producto: ${producto.nombre}</p>
                            <b> $ ${producto.precio}</b>`;
    document.body.appendChild(contenedor);
}
```

Código de clase

html

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <!-- css bootstrap -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-+0n0xVW2eSR5OomGNYDnhzAbDsOXxcvSN1TPprVMTNDbiYZCxYbOOl7+AMvyTG2x" crossorigin="anonymous">
    <title>Clase 8 - DOM</title>
</head>

<body>
    <section id="superior">
        <article>
            <a id="colores" href="http://www.coderhouse.com" target="_blank">Web de coder!</a>
        </article>
        <button onclick="cambiarVinculo()">Cambiar texto y color al link</button>
        <p>Buenas tardes a todos</p>
        <p>Buenas noches a todos</p>
        <button onclick="activarParrafos()">Cambiar parrafos</button>
    </section>

    <section id="inferior">
        <article id="aca"></article>
        <input id="nombre" type="text" placeholder="aqui nombre">
        <input id="edad" type="number" placeholder="aqui edad">
    </section>
    <!-- CDN BOOTSTRAP -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.1/dist/js/bootstrap.bundle.min.js" integrity="sha384-gtEjrD/SeCtmISkJkNUaaKMoLD0//ElJ19smozuHV6z3Iehds+3Ulb9Bn9Plx0x4" crossorigin="anonymous"></script>
    <script src="script.js"></script>
</body>

</html>
```

javascript

```javascript
//DOM
console.dir(document.body);

let seccionSuperior = document.getElementById("superior");
console.log(seccionSuperior.innerHTML);
seccionSuperior.style.background = "grey";

let vinculo = document.getElementById("colores");
console.log(vinculo.innerText);
vinculo.style.font = "italic bold 20px arial";

function cambiarVinculo() {
    //realizamos modificaciones en el HTML, puntualmente en <a> con id=colores
    vinculo.style.background = "yellow";
    vinculo.innerText = prompt("Ingresa texto para el vinculo");
}

function activarParrafos() {
    //realizamos modificaciones en el HTML, puntualmente en <p>
    let parrafos = document.getElementsByTagName("p");
    //console.log(parrafos);
    parrafos[0].style.background = "green";
    parrafos[1].innerText = "Cambiando desde JS";
    parrafos[1].style.font = "italic bold 30px Georgia";

}
//createElement && appendChild
let tit = document.createElement("h1");
tit.innerText = "Hola soy un titular dinamico";
document.getElementById("inferior").appendChild(tit);

//boton dinamico
let nuevoBoton = document.createElement("button");
nuevoBoton.innerText = "Borrar el H1 dinamico";
nuevoBoton.setAttribute("onclick", 'tit.parentNode.removeChild(tit)');
document.getElementById("inferior").appendChild(nuevoBoton);

//plantillas
const productos = [{ id: 1, nombre: "Arroz", precio: 125 },
    { id: 2, nombre: "Fideo", precio: 70 },
    { id: 3, nombre: "Pan", precio: 50 },
    { id: 4, nombre: "Flan", precio: 100 }
];

for (const producto of productos) {
    let contenedor = document.createElement("div");
    //Definimos el innerHTML del elemento con una plantilla de texto
    contenedor.innerHTML = `<h3> ID: ${producto.id}</h3>
                            <p>  Producto: ${producto.nombre}</p>
                            <b> $ ${producto.precio}</b>`;
    document.body.appendChild(contenedor);
}
```
