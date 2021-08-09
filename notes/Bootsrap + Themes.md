---
tags: [Coderhouse, CSS]
title: Bootsrap + Themes
created: '2021-05-07T04:12:37.754Z'
modified: '2021-07-02T21:45:06.334Z'
---

# Bootsrap + Themes

## Bootstrap

### Conociendo bootstrap

Adapta la interfaz del sitio web al tamaño del dispositivo en que se visualice (es responsive).

### Como visualizar Bootstrap

- index.html
- css/
	- bootstrap.css
    - bootstrap-responsive.css
- js/
	- bootstrap.js

### Instalar Bootstrap

1. Código compilado listo para usar para Bootstrap .
2. Archivos para compilar.
3. BootstrapCDN (enlace directo).
4. Instalando paquetes.

Vamos a usar las formas más sencillas:
- Descargando los archivos.
- Con el enlace a los archivos.

### Instalando el compilado

#### Forma 1
- se descarga el compilado
- se descompila
- se lleva a la carpeta del proyecto

#### Forma 2
- se copia el CDN
- se pega en el head del documento

### Mobile first - Bootstrap
Para garantizar una representación adecuada, y un zoom táctil para todos los dispositivos, no olvides agregar el viewport:

```html

<meta name="viewport" content="width=device-width, initial-scale=1">

```

### Tipografia en bootstrap
Todos los tags de \<h1> a \<h6> están estilados por Bootstrap. También se puede utilizar el tag \<small> para mostrar un texto secundario

#### Clase "lead"
Sirve para destacar un párrafo
```html

 <p class="lead"">Aquí va el contenido en un container fluid con clase lead.</p>
```

### Contenedores

#### clase "container"
Cada contenedor tiene un ancho variable, que va a depender de la resolución de pantalla del usuario. Esto lo averiguará Bootstrap, y va a setearle el ancho correspondiente. 
```html
<div class="container">
  <h1>Título Principal</h1>
  <p>Aquí va el contenido.</p>
</div>
```
#### clase "container-fluid"
El ancho siempre será de 100%, **brindándonos la posibilidad renderizar un div full width**.
```html
<div class="container-fluid"">
  <h1>Título Principal</h1>
  <p>Aquí va el contenido.</p>
</div>
```
#### clase "row"
**Serán las filas en donde dividiremos el contenido del bloque**, que reacomodará los divs de su interior dependiendo siempre de la resolución del usuario.

```html
<h1>Título Principal</h1>
<div class="container">
<div class="row">
  <p>Aquí va el contenido.</p>
</div>
</div>
```

### Sistema de grillas
**La grilla se divide en 12 columnas**, que varían su ancho dependiendo de la resolución del usuario móvil, o de escritorio.
Estas columnas se ubican siempre dentro de una fila, el div .row mencionado anteriormente.
Se representa como col-md-x que indica que el div ocupará X columnas en un .container.

Si quisiéramos que el mismo div ocupe 6 columnas en un dispositivo de 480px de ancho, deberíamos aplicarle dos clases, para indicarle **un comportamiento para cada resolución**, como se visualiza en el siguiente ejemplo:

```html
<div class="container">
<div class="row">
     <div class="col-md-4 col-xs-6">columna izquierda</div>
</div>
</div>
```

| Extra small   | Small        | Medium       | Large           | Extra large      |
| ----------   | -----        | ------       | -----           | -----------      |
|less than 576px | 576px and up | 768px and up | min width 992px | min width 1200px |
|  default | .col-xs- | -col-sn- | .col-md- | .col-lg |

**Se puede nombrar un div con dos clases diferentes**, que proporcionarán distintos estilos al mismo elemento.

```html
<div class="col-md-4 col-sm-6">

```

### Tablas
```html
<h1>Título Principal</h1>
<div class="container">
 <h2>Tabla Básica</h2>
  <p>La clase .table agrega un estilo básico (relleno ligero y solo divisores horizontales) a una tabla:</p>       	 
  <table class="table">
          ….
 </table>
</div>
```

### Formularios
Bootstrap aplica por defecto algunos estilos a todos los componentes de los formularios. Si además añades la clase **.form-control** a los elementos \<input>, \<textarea> y \<select>, su anchura se establece a width: 100%. 
Si quieres optimizar el espaciado, utiliza la **clase .form-group** para encerrar cada campo de formulario con su \<label>.

```html
<h1>Título Principal</h1>
<div class="container">
 <h2>Formulario Básico</h2>
  <form action="#">
	<div class="form-group">
  	<label for="email">Email:</label>
  	<input type="email" class="form-control" id="email" placeholder="Ingrese email" name="email">
	</div>
           …..
	<button type="submit" class="btn btn-default">
                Ingresar
           </button>
  </form>
</div>
```
### Imagenes
```html
<img src="obelisco.jpg" class="img-rounded" alt="Obelisco BsAs">

<img src="obelisco.jpg" class="img-circle" alt="Obelisco BsAs">

<img src="obelisco.jpg" class="img-thumbnail" alt="Obelisco BsAs">
```

### Dropdowns
```html
  <div class="dropdown">
	<button type="button" class="btn btn-primary dropdown-toggle" data-toggle="dropdown">
  	Elige una opción:
	</button>
	<div class="dropdown-menu">
  	<a class="dropdown-item" href="#">Opción uno</a>
  	<a class="dropdown-item" href="#">Opción dos</a>
  	<a class="dropdown-item" href="#">Opción tres</a>
	</div>
  </div>
```
### Estilo de botones
```html
<div class="btn-group-vertical"> <!-- Agrupando botones verticalmente -->
  <h2>Estilo de Botones</h2>
  <button type="button" class="btn">Básico</button>
  <button type="button" class="btn btn-primary">Primario</button>
  <button type="button" class="btn btn-secondary">Secundario</button>
  <button type="button" class="btn btn-success">Exitoso</button>
  <button type="button" class="btn btn-info">Info</button>
  <button type="button" class="btn btn-warning">Advertencia</button>
  <button type="button" class="btn btn-danger">Peligroso</button>
  <button type="button" class="btn btn-dark">Oscuro</button>
  <button type="button" class="btn btn-light">Claro</button>
  <button type="button" class="btn btn-link">Enlace</button> 	 
</div>
</div>
```

### Grupos de botones
```html
<div class="btn-group">
	<button type="button" class="btn btn-primary">Inicio</button>
	<button type="button" class="btn btn-primary">Quienes Somos</button>
	<div class="btn-group">
  	<button type="button" class="btn btn-primary dropdown-toggle" data-toggle="dropdown">
  	Integrantes
  	</button>
  	<div class="dropdown-menu">
    	<a class="dropdown-item" href="#">Cantante</a>
    	<a class="dropdown-item" href="#">Bajo</a>
  	</div>
	</div>
  </div>

```
### Paginación
```html
  <ul class="pagination">
	<li class="page-item"><a class="page-link" href="#">Anterior</a></li>
	<li class="page-item"><a class="page-link" href="#">1</a></li>
	<li class="page-item"><a class="page-link" href="#">2</a></li>
	<li class="page-item"><a class="page-link" href="#">3</a></li>
	<li class="page-item"><a class="page-link" href="#">Siguiente</a></li>
  </ul>
```
### Nav menú
```html
<div class="container">
  <p>Menú básico horizontal:</p>
  <ul class="nav">
	<li class="nav-item">
  	<a class="nav-link" href="#">Inicio</a>
	</li>
	<li class="nav-item">
  	<a class="nav-link" href="#">Quienes Somos</a>
	</li>
	<li class="nav-item">
  	<a class="nav-link" href="#">Historia</a>
	</li>
	<li class="nav-item">
  	<a class="nav-link disabled" href="#">Newlestter</a>
	</li>
  </ul>
</div>
```
## Bootstrap con Javascript
**Muchos de los componentes de Bootstrap requieren el uso de JavaScript para funcionar. Específicamente, requieren jQuery, Popper.js y complementos propios de JavaScript.** 

Para eso hay que colocar los \<script> vistos en la clase anterior, cerca del final de las páginas, **justo antes de la etiqueta de cierre del \</body>**, para habilitarlas. jQuery debe ser lo primero, luego Popper.js, y luego nuestros complementos de JavaScript.

**Para que puedas incluir en tu proyecto componentes tales como carrusel o menú con drop down, tienes que sumar al final de tus html tres links antes del cierre de la etiqueta body de la siguiente manera:**
 ```html
<body> (…)
<script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
<script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.0/dist/umd/popper.min.js" integrity="sha384-Q6E9RHvbIyZFJoft+2mJbHaEWldlvI9IOYy5n3zV9zzTtmI3UksdQRVvoxMfooAo" crossorigin="anonymous"></script>
<script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/js/bootstrap.min.js" integrity="sha384-OgVRvuATP1z7JjHLkuOU7Xw704+h835Lr+6QL9UvYjZE3Ipu6Tp75j7Bh/kR0JKI" crossorigin="anonymous"></script>
</body>
 ```
### Budges
```html
<h2>Título de ejemplo 
<span class="badge badge-secondary"> Nuevo </span> </h2>
<h3>Título de ejemplo <span class="badge badge-secondary"> Nuevo </span></h3>
```
### Mensajes POPOVER
```html
<div id="demo" class="collapse">
<a href="#" title="Título" data-toggle="popover" data-placement="left" data-content="Contenido">Izquierda</a>
<a href="#" title="Título" data-toggle="popover" data-placement="right" data-content="Contenido">Derecha</a>
```
### Mensajes colapsados
``` html
<button type="button" class="btn btn-primary" data-toggle="collapse" data-target="#demo">
Click acá </button>
<div id="demo" class="collapse"> Texto desplegado a continuación: Lorem ipsum dolor sit amet, consectetur adipisicing elit. </div>
```
### Breadcrumb
```html
  <ol class="breadcrumb">
    <li class="breadcrumb-item"><a href="#">Home</a></li>
    <li class="breadcrumb-item"><a href="#">Nosotros</a></li>
    <li class="breadcrumb-item active" aria-current="page">Contacto</li>
  </ol>
```

## Bootstrap Themes
**Permiten tener un diseño base como una extensión de Bootstrap**, especialmente para un conjunto específico de problemas. Esto significa que no sólo extiende los componentes básicos de Bootstrap, **sino que también se pueden agregar componentes, utilidades y complementos completamente nuevos.**

**En Bootstrap 4, los temas se crean con variables Sass, mapas Sass y código CSS propio.** 
Se recomienda utilizar los archivos Sass (que veremos más adelante) incluidos en Bootstrap, para reutilizar todas las variables, mapas y mixins que puedas.

- tu-proyecto/
	- scss/
		- custom.scss
	- node_modules/
		- bootstrap/
			- js
			- scss
1. Busca el tema de preferencia, Bootstrap Oficial, Otras Páginas
2. Seleccionar el tema, y descarga el .zip a la carpeta local
3. Adapta el theme a tus necesidades

### Editando un theme
Tener un theme es tan simple como descargarlo, y ya se tiene una página web completa.
**Para editarlo, sólo se debe revisar cada HTML y cambiar el contenido, si se desea cambiar el diseño hay que usar el SASS.**

### Ventajas y desventajas de un theme

#### Ventajas
- Se crea un sitio web de una forma rápida.
- Componentes incorporados.
- Fácil manejo de cada una de las páginas.
- Responsive.
- Mobile First.
- Óptimo.
- Base para un nuevo Theme.
#### Desventajas
- Se escapan detalles de diseño.
- Hay que ser muy detallista para cambiar todo el contenido del theme.
- Es complicado cambiar de versión.
- Si necesitas añadir componentes que no existen, debes hacerlo tú mismo/a en CSS, cuidando que mantenga coherencia con el diseño y sea responsive.

