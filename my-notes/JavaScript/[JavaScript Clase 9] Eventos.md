---
tags: [Coderhouse, JavaScript]
title: '[JavaScript Clase 9] Eventos'
created: '2021-07-07T23:30:56.216Z'
modified: '2021-07-20T14:46:02.072Z'
---

# [JavaScript Clase 9] Eventos

Los eventos son la manera que tenemos en Javascript de **controlar las acciones de los usuarios**, y definir un comportamiento de la página o aplicación cuando se produzcan. 

Con Javascript podemos definir qué es lo que pasa cuando se produce un evento, cómo podría ser un clic en cierto elemento, o escribir en un campo.

### Funcionamiento

JavaScript permite **asignar una función a cada uno de los eventos**. 
De esta forma, cuando se produce cualquier evento, JavaScript ejecuta su función asociada. Este tipo de funciones se denominan **event handlers** en inglés, y en castellano por "manejadores de eventos".
Los eventos se asocian a cada elemento al cual se lo quiere "escuchar".

## Definir eventos

### Opción 1

El método **addEventListener()** permite definir qué evento escuchar sobre cualquier elemento en el código HTML.
El **primer parámetro corresponde al nombre del evento y el segundo a la función de respuesta.**

- Se mete el objeto tomado por ID y se le agrega el método addEventListener()
- addEventListener() toma como primer parámetro el tipo de evento
- addEventListener() toma como segundo parámetro el nombre de la funcion a ejecutar

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Mi primer App</title>
  </head>
  <body>
    <h2>Coder House</h2>
    <button id="btnPrincipal">CLICK</button>
    <script>
      let boton = document.getElementById("btnPrincipal")
      boton.addEventListener("click", respuestaClick)
      function respuestaClick(){
        console.log("Respuesta evento");
      }
    </script>
  </body>
</html>
```

### Opción 2

**Emplear una propiedad del nodo para definir la respuesta al evento**. Las propiedades se identifican con el nombre del evento y el prefijo on. También es posible emplear funciones anónimas para definir los manejadores de eventos.

- Se mete el objeto tomado por ID
- Se ejecuta la propiedad del nodo. Ej = onclick = function()
- 

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Mi primer App</title>
  </head>
  <body>
    <h2>Coder House</h2>
    <button id="btnPrincipal">CLICK</button>
    <script>
      let boton = document.getElementById("btnPrincipal")
      boton.onclick = () =>{console.log("Respuesta 2")}
    </script>
  </body>
</html>
```

### Opción 3

**Determinar el evento especificando el Event Handler en el atributo de una etiqueta HTML**. La denominación del atributo es idéntica al de la propiedad de la opción 2 (prefijo on)

```html
 <input type="button" value="CLICK2" onclick="alert('Respuesta 3');" />
```
La función puede declararse entre la comillas o bien tomarse una referencia existen en el script.

**Las opciones 1 y 2 son las recomendadas**, si bien se pueden presentar casos de aplicación específico (por ejemplo, en la opción 1 el nombre del evento puede venir de una variable al usar la propiedad, y esto no puede hacerse en la 2), se identifican como formas de definición de evento equivalentes. 
La opción 3, aunque es de fácil implementación, no es recomendada para proyectos en producción ya que no es considerada un buena práctica declarar funciones y código JavaScript dentro del HTML.

## Eventos mas comúnes

### Eventos con el MOUSE

Los eventos del mouse o MouseEvent son aquellos que **se producen por la interacción del usuario con el mouse**. Entre ellos destacamos:
- **mousedown/mouseup**: Se oprime/suelta el botón del ratón sobre un elemento.
- **mouseover/mouseout**:  El puntero del mouse se mueve sobre/sale del elemento.
- **mousemove**: El movimiento del mouse sobre el elemento activa el evento.
- **click**: Se activa después de mousedown o mouseup sobre un elemento válido.

```html 
//CODIGO HTML DE REFERENCIA
<button id="btnMain">CLICK</button>
```

```javascript
//CODIGO JS
let boton         = document.getElementById("btnMain");
boton.onclick     = () => {console.log("Click")};
boton.onmousemove = () => {console.log("Move")}
```

### Eventos del teclado

Los eventos de teclado o **KeyboardEvent** describen una interacción del usuario con el teclado son aquellos que se producen por la **interacción del usuario con el teclado**. Entre ellos destacamos:
- **keydown**: Cuando se presiona.
- **keyup**: Cuando se suelta una tecla.

```html
//CODIGO HTML DE REFERENCIA
<input id = "nombre" type="text">
<input id = "edad"   type="number">
```
```javascript
//CODIGO JS
let input1  = document.getElementById("nombre");
let input2  = document.getElementById("edad");
input1.onkeyup   = () => {console.log("keyUp")};
input2.onkeydown = () => {console.log("keyDown")};
```

### Evento CHANGE

El evento change **se activa cuando se detecta un cambio en el valor del elemento**. 
Por ejemplo, mientras estamos escribiendo en un input de tipo texto, no hay evento change, pero cuando pasamos a otra sección de la aplicación entonces ocurre el evento change.

```html
//CODIGO HTML DE REFERENCIA
<input id = "nombre" type="text">
<input id = "edad"   type="number">
```
```javascript
//CODIGO JS
let input1  = document.getElementById("nombre");
let input2  = document.getElementById("edad");
input1.onchange = () => {console.log("valor1")};
input2.onchange = () => {console.log("valor2")};
```

### Evento SUBMIT

El evento submit **se activa cuando el formulario es enviado**, normalmente se utiliza para validar el formulario antes de ser enviado al servidor o bien para abortar el envío y procesarlo con JavaScript.

```html
//CODIGO HTML DE REFERENCIA
 <form id="formulario">
      <input type="text">
      <input type="number">
      <input type="submit" value="Enviar">
 </form>
 ```

```javascript
//CODIGO JS DE REFERENCIA
let miFormulario = document.getElementById("formulario");
miFormulario.addEventListener("submit", validarFormulario);

function validarFormulario(e){
    e.preventDefault();
    console.log("Formulario Enviado");    
}
```

### Otros eventos

Existen otros eventos que podemos utilizar. Algunos son eventos estándar definidos en las especificaciones oficiales, mientras que otros son eventos usados internamente por navegadores específicos.

La forma de declararlos es similar a lo abordado en esta clase, lo que necesitamos aprender es bajo qué condición se disparan los eventos que buscamos implementar.
Para conocer más eventos se recomienda verificar la referencia de eventos en la documentación.

### Informacion del evento

En algunos casos, necesitamos obtener información contextual del evento para poder realizar acciones. Por ejemplo, ante el evento submit necesitamos prevenir el comportamiento por defecto para operar correctamente. 
**Para esto existe en JavaScript el objeto EVENT**.
**En todos los navegadores modernos se crea de forma automática un parámetro que se pasa a la función manejadora, por lo que no es necesario incluirlo en la llamada.**
Ese parámetro puede o no usarse en el evento, pero siempre estará disponible en la llamada.

#### Ejemplo aplicado

```html
//CODIGO HTML DE REFERENCIA
 <form id="formulario">
      <input type="text">
      <input type="number">
      <input type="submit" value="Enviar">
    </form>
```

```javascript
//CODIGO JS
let miFormulario      = document.getElementById("formulario");
miFormulario.addEventListener("submit", validarFormulario);

function validarFormulario(e){
    //Cancelamos el comportamiento del evento
    e.preventDefault();
    //Obtenemos el elemento desde el cual se disparó el evento
    let formulario = e.target
    //Obtengo el valor del primero hijo <input type="text">
    console.log(formulario.children[0].value); 
    //Obtengo el valor del segundo hijo <input type="number"> 
    console.log(formulario.children[1].value);  
}
```

## Código en clase

```html

HTML

<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Clase 9</title>
</head>

<body>
    <section>
        <button id="miBoton">INTERACTUAR</button>
        <p></p>
        <form id="formulario">
            <input id="edad" type="text" placeholder="ingresa tu edad" onchange="activarFrase(this)">
            <!--  -->
            <input type="text" placeholder="ingresa tu nombre" onkeypress="capturarEnter(event)">
            <!--  -->
            <input type="submit" value="Enviar">
        </form>
        <p class="textoP">Trata de copiar éste texto</p>
    </section>
    <script src="script.js"></script>
</body>

</html>
```

Código de clase

```javascript
//Javascript

//Eventos

function interactuar() {
    let nombre = prompt("Ingresa tu nombre");
    let fecha = new Date();
    alert("Hola " + nombre + " te informo que hoy es: " + fecha);
}

//opcion1
// let boton = document.getElementById("miBoton");
// boton.addEventListener("click", interactuar); //ojo con la funcion

//opcion2
let boton2 = document.getElementById("miBoton");
boton2.onclick = () => { console.log("click"); }
boton2.onmousemove = () => { console.log("move"); }

//eventos de teclado
// let campoEdad = document.getElementById("edad");
// campoEdad.onkeyup = () => { console.log("keyUp"); }
// campoEdad.onkeydown = () => { console.log("keyDown"); }
// campoEdad.onchange = () => { console.log("la edad cambió!"); }

let miFormulario = document.getElementById("formulario");
miFormulario.addEventListener("submit", validarFormulario);

function validarFormulario(e) {
    e.preventDefault(); //evita que se borren los campos
    console.log(e);
    //aqui validaciones
}

//Evento extra bonus track (clipboard)
let textoParaNoCopiar = document.getElementsByClassName("textoP"); //array
textoParaNoCopiar[0].addEventListener("copy", imprimirAlerta);

function imprimirAlerta() {
    console.log("Ojo que vi que te copiaste!!!!");
}

//opcion 3
function activarFrase(entrada) {
    //console.log(entrada);
    let edad = entrada.value;
    //console.log("La edad ingresada es: " + edad);
    if (edad < 1 || edad > 100) {
        alert("Edad invalida");
    }
}

function capturarEnter(evento) {
    if (evento.which == 13 || evento.keyCode == 13) {
        alert("Presionaste ENTER");
    }
}```
